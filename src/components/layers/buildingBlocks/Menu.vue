<template>
    <ul class="menu w-full">
        <li class="menu-title">
            <slot name="header"></slot>
        </li>
        <li v-for="child in $slots.default?.()" class="flex">
            <component :is="child"></component>
        </li>
    </ul>
</template>