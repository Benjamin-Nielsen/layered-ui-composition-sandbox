<template>
    <div role="tablist" class="tabs tabs-lift">
        <template v-for="(child, i) in $slots.default?.()" :key="i">
            <input type="radio" name="tabs" role="tab" class="tab" :aria-label="'Tab ' + i"
                :checked="i === 0 ? 'checked' : null">
            <div class="tab-content bg-base-100 border-base-300 p-6">
                <component :is="child" />
            </div>
        </template>
    </div>
</template>
