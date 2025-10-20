<script setup>
import { ref } from 'vue';
import Card from '../layers/buildingBlocks/Card.vue';
import RangeIndicator from '../layers/forms/RangeIndicator.vue';
import Cog from '../icons/Cog.vue';

const range = ref(50);
</script>
<template>
    <Card>
        <h2 class="flex items-center justify-between"><span class="flex items-center gap-2 font-semibold">
                <Cog></Cog> Range indicator
            </span></h2>
        <div class="text-center text-5xl font-extralight">{{ range }}</div>
        <RangeIndicator v-model="range"></RangeIndicator>
    </Card>
</template>