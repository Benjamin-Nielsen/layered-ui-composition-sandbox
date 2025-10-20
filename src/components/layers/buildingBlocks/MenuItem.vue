<template>
    <div class="flex gap-1 w-full items-center">
        <slot name="icon"></slot>
        <div class="grow">
            <slot class="grow"></slot>
        </div>
        <slot name="right"></slot>
    </div>
</template>
