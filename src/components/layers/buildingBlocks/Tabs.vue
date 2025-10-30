<script setup>
const props = defineProps({
    uniqueName: {
        type: String,
        required: false,
        default: 'tabs-' + Math.random().toString(36).substring(2, 15),
    },
});
</script>
<template>
    <div role="tablist" class="tabs tabs-lift">
        <template v-for="(child, i) in $slots.default?.()" :key="i">
            <input type="radio" :name="uniqueName" role="tab" class="tab" :aria-label="child.props?.title"
                :checked="i === 0 ? 'checked' : null">
            <div class="tab-content bg-base-100 border-base-300 p-6">
                <component :is="child" />
            </div>
        </template>
    </div>
</template>
