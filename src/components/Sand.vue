<script setup>
import { ref } from "vue";
import { getDaisyUiLinks } from "../functions/getDaisyUiLinks.js";
import Card from "./layers/buildingBlocks/Card.vue";
import PenAndPaper from "./icons/PenAndPaper.vue";
import FitTextDemo from "./examples/FitTextDemo.vue";
import MenuDemo from "./examples/MenuDemo.vue";
import PostDemo from "./examples/PostDemo.vue";
import TimelineDemo from "./examples/TimelineDemo.vue";
import FormDemo from "./examples/FormDemo.vue";
import RangeIndicatorDemo from "./examples/RangeIndicatorDemo.vue";

const range = ref(50);

</script>

<template>
  <main>
    <Card class="mb-4">
      <div class="text-2xl font-bold pb-2">Layered UI Composition Pattern</div>
      <div class="text-xl pb-2">Look at all the nice things we can make!</div>

      <div class="flex flex-col gap-2">
        <a v-for="(link, i) in getDaisyUiLinks()" :href="link">
          <span class="flex gap-1 align-items-center">
        <PenAndPaper></PenAndPaper>DaisyUI Template {{ i + 1 }}
      </span>
        </a>
      </div>
      <div>TODO Make a FlowGridComponent</div>
      <div>TODO Reuse components in the various demos</div>
    </Card>
    <div
      class="text-base-content mx-auto grid grid-cols-1 xs:grid-cols-1 gap-6 pb-20 sm:grid-cols-2 md:grid-cols-2 lg:grid-cols-3 [&>*]:mb-6">
      <div class="flex flex-col gap-4">
        <FormDemo></FormDemo>
        <FitTextDemo></FitTextDemo>
      </div>
      <div class="flex flex-col gap-4">
        <RangeIndicatorDemo></RangeIndicatorDemo>
        <TimelineDemo></TimelineDemo>
        <PostDemo></PostDemo>
      </div>
      <div class="flex flex-col gap-4">
        <MenuDemo></MenuDemo>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
