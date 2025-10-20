<script setup>
import { ref } from 'vue';
import Card from "../layers/buildingBlocks/Card.vue";
import PenAndPaper from "../icons/PenAndPaper.vue";
import RangeIndicator from '../layers/forms/RangeIndicator.vue';
import FitText from '../layers/transformers/FitText.vue';

const fitTextTitle = ref("This is a title to test the FitText component");
const fitTextHeight = ref(500);
const fitTextMax = ref(68);
const fitTextMin = ref(8);
const fontSize = ref(0);
</script>
<template>
    <Card>
          <template #header>
            <PenAndPaper></PenAndPaper>
            Test of the FitText component
          </template>
          <Card>
            <template #header>Fit text</template>
            Title <input type="string" v-model="fitTextTitle"/>
            Height ({{ Number(fitTextHeight) }}px)
            <RangeIndicator v-model="fitTextHeight" max="1000" min="50"></RangeIndicator>
            Min ({{ Number(fitTextMin) }}px)
            <RangeIndicator v-model="fitTextMin" max="100" min="8"></RangeIndicator>
            Max ({{ Number(fitTextMax) }}px)
            <RangeIndicator v-model="fitTextMax" max="100" min="8"></RangeIndicator>
          </Card>
          <FitText :style="{ height: fitTextHeight + 'px' }" @update:fontSize="fontSize = $event" :max="Number(fitTextMax)" :min="Number(fitTextMin)">
            <div class="text-l">{{ fitTextTitle }}</div>
          </FitText>
          <p class="text-sm text-gray-500 mt-1">
            Font size: {{ fontSize }}px
          </p>
          <div>Min: {{ fitTextMin }}px</div>
          <div>Max: {{ fitTextMax }}px</div>
        </Card>
    </template>