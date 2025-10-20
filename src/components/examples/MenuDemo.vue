<script setup>
import Database from "../icons/Database.vue";
import Box from "../icons/Box.vue";
import Letter from "../icons/Letter.vue";
import SlidingToggles from "../icons/SlidingToggles.vue";
import Menu from "../layers/buildingBlocks/Menu.vue";
import MenuItem from "../layers/buildingBlocks/MenuItem.vue";

const handleSettingsClick = () => {
    console.log("Clicked settings!");
};
</script>
<template>
    <div class="card card-border border-base-300 bg-base-100">
        <Menu>
            <template #header>Menu panel</template>
            <a href="#" class="flex grow">
                <MenuItem>
                <template #icon>
                    <Database></Database>
                </template>
                <span>
                    Databases
                </span>
                <template #right>
                    <span class="badge justify-self-end text-sm">7</span>
                </template>
                </MenuItem>
            </a>
            <a href="#">
                <MenuItem>
                <template #icon>
                    <Box></Box>
                </template>
                Products
                </MenuItem>
            </a>
            <a href="#" class="flex grow">
                <MenuItem>
                <template #icon>
                    <Letter></Letter>
                </template>
                Messages
                <template #right>
                    <span class="badge justify-self-end">29</span>
                </template>
                </MenuItem>
            </a>
            <button @click="handleSettingsClick">
                <MenuItem>
                <template #icon>
                    <SlidingToggles></SlidingToggles>
                </template>
                Settings
                </MenuItem>
            </button>
        </Menu>
    </div>
</template>