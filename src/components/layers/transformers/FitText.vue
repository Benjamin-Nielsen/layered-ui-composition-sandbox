<script setup>
import { ref, reactive, computed, onMounted, onBeforeUnmount, nextTick, watch } from 'vue'

const props = defineProps({
  min: { type: Number, default: 8 },
  max: { type: Number, default: 48 },
  precision: { type: Number, default: 0.5 },
  lineHeight: { type: [Number, String], default: 1.2 },
  debounceMs: { type: Number, default: 50 },
  preferWholePixels: { type: Boolean, default: false },
  clampLines: { type: Number, default: null },
  ellipsis: { type: Boolean, default: false },
  debug: { type: Boolean, default: false },
})

const emit = defineEmits(['update:fontSize', 'fit'])

const host = ref(null)
const sizer = ref(null)

const currentFontSize = ref(Math.min(24, props.max))
const didFit = ref(true)
const hostSize = reactive({ w: 0, h: 0 })

const sizerStyle = computed(() => {
  const lh = typeof props.lineHeight === 'number' ? `${props.lineHeight}` : props.lineHeight
  const clamp =
    props.clampLines && props.clampLines > 0
      ? {
          display: '-webkit-box',
          WebkitBoxOrient: 'vertical',
          WebkitLineClamp: String(props.clampLines),
          overflow: 'hidden',
        }
      : {}

  const textOverflow =
    props.ellipsis && props.clampLines === 1
      ? { whiteSpace: 'nowrap', textOverflow: 'ellipsis', overflow: 'hidden' }
      : {}

  return {
    fontSize: `${currentFontSize.value}px`,
    lineHeight: lh,
    width: '100%',
    paddingTop: '0.001px',
    paddingBottom: '0.001px',
    ...clamp,
    ...textOverflow,
  }
})

const raf = (fn) => {
  let id = 0
  return (...args) => {
    cancelAnimationFrame(id)
    id = requestAnimationFrame(() => fn(...args))
  }
}

let ro = null
let mo = null
let io = null
let debounceTimer = null

function scheduleFit(immediate = false) {
  if (!host.value || !sizer.value) return
  if (immediate) {
    fitNow()
    return
  }
  if (debounceTimer) window.clearTimeout(debounceTimer)
  debounceTimer = window.setTimeout(() => fitNow(), props.debounceMs)
}

const fitNow = raf(async () => {
  if (!host.value || !sizer.value) return
  await nextTick()

  const rect = host.value.getBoundingClientRect()
  hostSize.w = Math.max(0, Math.floor(rect.width))
  hostSize.h = Math.max(0, Math.floor(rect.height))
  if (hostSize.w === 0 || hostSize.h === 0) return

  let low = props.min
  let high = props.max
  let best = props.min

  setFontSize(high)
  await nextTick()

  if (fitsContainer()) {
    best = high
  } else {
    setFontSize(low)
    await nextTick()

    if (!fitsContainer()) {
      best = low
      didFit.value = false
      finalize(best)
      return
    }

    while (high - low > props.precision) {
      const mid = (low + high) / 2
      setFontSize(mid)
      await nextTick()

      if (fitsContainer()) {
        best = mid
        low = mid
      } else {
        high = mid
      }
    }
  }

  didFit.value = true
  finalize(best)
})

function setFontSize(sz) {
  currentFontSize.value = sz
}

function fitsContainer() {
  const el = sizer.value
  const hostEl = host.value
  const EPS = 0.5

  if (props.ellipsis && props.clampLines === 1) {
    return (
      el.scrollWidth <= hostEl.clientWidth + EPS &&
      el.scrollHeight <= hostEl.clientHeight + EPS
    )
  }

  const okW = el.scrollWidth <= hostEl.clientWidth + EPS
  const okH = el.scrollHeight <= hostEl.clientHeight + EPS
  return okW && okH
}

function finalize(best) {
  const finalSize = props.preferWholePixels ? Math.floor(best) : best
  setFontSize(finalSize)
  emit('update:fontSize', finalSize)

  const hostEl = host.value
  emit('fit', {
    fontSize: finalSize,
    width: hostEl.clientWidth,
    height: hostEl.clientHeight,
    fits: didFit.value,
  })
}

onMounted(() => {
  if (!host.value || !sizer.value) return

  ro = new ResizeObserver(() => scheduleFit())
  ro.observe(host.value)

  mo = new MutationObserver(() => scheduleFit())
  mo.observe(sizer.value, { childList: true, characterData: true, subtree: true, attributes: true })

  io = new IntersectionObserver((entries) => {
    for (const e of entries) {
      if (e.isIntersecting) scheduleFit(true)
    }
  }, { threshold: 0.01 })
  io.observe(host.value)

  scheduleFit(true)
  window.addEventListener('load', handleWindowLoad, { passive: true })
})

onBeforeUnmount(() => {
  ro && ro.disconnect()
  mo && mo.disconnect()
  io && io.disconnect()
  window.removeEventListener('load', handleWindowLoad)
  if (debounceTimer) window.clearTimeout(debounceTimer)
})

function handleWindowLoad() {
  scheduleFit(true)
}

watch(
  () => [
    props.min,
    props.max,
    props.precision,
    props.lineHeight,
    props.clampLines,
    props.ellipsis,
    props.preferWholePixels,
  ],
  () => scheduleFit(true),
  { deep: true }
)
</script>

<template>
  <div ref="host" class="fittext-host">
    <div
      ref="sizer"
      class="fittext-sizer"
      :style="sizerStyle"
      aria-live="polite"
    >
      <slot></slot>
    </div>

    <div v-if="debug" class="fittext-debug">
      <div>fs: {{ currentFontSize.toFixed(2) }}px</div>
      <div>w×h: {{ hostSize.w }}×{{ hostSize.h }}</div>
      <div>fits: {{ didFit ? 'yes' : 'no' }}</div>
    </div>
  </div>
</template>

<style scoped>
.fittext-host {
  position: relative;
  display: block;
  width: 100%;
  height: 100%;
  overflow: hidden;
  transition: height 0.3s ease;
}

.fittext-sizer {
  display: block;
  width: 100%;
  min-width: 0;
}

.fittext-debug {
  position: absolute;
  right: 4px;
  bottom: 4px;
  background: rgba(0, 0, 0, 0.55);
  color: #fff;
  font-family: monospace;
  font-size: 10px;
  padding: 4px 6px;
  border-radius: 4px;
  pointer-events: none;
}
</style>
