<script setup>
</script>
<template>
    <div class="card bg-base-100 card-border border-base-300 card-sm">
        <div v-if="$slots.header">
            <div class="border-base-300 border-b border-dashed">
                <div class="flex items-center gap-2 p-4">
                    <div class="grow">
                        <div class="flex items-center gap-2 text-sm font-medium">
                            <slot name="header"></slot>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="card-body gap-4">
            <slot></slot>
        </div>
    </div>
</template>