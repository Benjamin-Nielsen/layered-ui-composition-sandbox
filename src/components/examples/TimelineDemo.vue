<script setup>
import { reactive } from 'vue';
import Card from '../layers/buildingBlocks/Card.vue';
import Cog from '../icons/Cog.vue';
import Timeline from '../layers/buildingBlocks/Timeline.vue';

const timelineHighlights = reactive({});
</script>
<template>
    <Card>
        <template #header>
            <Cog></Cog>
            Timeline
        </template>
        <Timeline>
            <div :highlighted="timelineHighlights[0]" @click="timelineHighlights[0] = !timelineHighlights[0]">
                Test1<br />
                Test two lines
            </div>
            <button :highlighted="timelineHighlights[1]" @click="timelineHighlights[1] = !timelineHighlights[1]">
                <p>
                    Test2
                </p>
            </button>
            <button :highlighted="timelineHighlights[2]" @click="timelineHighlights[2] = !timelineHighlights[2]">
                <strong>
                    Test3
                </strong>
            </button>
            <button :highlighted="timelineHighlights[3]" @click="timelineHighlights[3] = !timelineHighlights[3]">
                <h2>
                    Test4
                </h2>
            </button>
        </Timeline>
    </Card>
</template>
