<script setup lang="ts">
import Checkmark from '../../icons/Checkmark.vue';

</script>

<template>
    <ul class="timeline timeline-vertical timeline-compact">
        <li v-for="(child, i) in $slots.default?.()" :key="i">
            <hr v-if="i > 0"
                :class="(child.props['highlighted'] && (i - 1 >= 0 && $slots.default?.()[i - 1].props['highlighted'])) ? 'bg-primary' : ''">
            <div class="timeline-middle">
                <Checkmark :highlighted="child.props['highlighted']"></Checkmark>
            </div>
            <div class="timeline-end timeline-box w-full">
                <!-- render the VNode directly -->
                <component :is="child" />
            </div>
            <hr v-if="i < $slots.default?.().length - 1"
                :class="(child.props['highlighted'] && (i + 1 < $slots.default?.().length && $slots.default?.()[i + 1].props['highlighted'])) ? 'bg-primary' : ''">
        </li>
    </ul>
</template>