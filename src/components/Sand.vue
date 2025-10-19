<script setup>
import { ref, reactive } from "vue";
import PrimaryInput from "./layers/PrimaryInput.vue";
import ErrorLabel from "./layers/ErrorLabel.vue";
import ScaleOnClick from "./layers/ScaleOnClick.vue";
import StrippedButton from "./layers/StrippedButton.vue";
import PrimaryButton from "./layers/PrimaryButton.vue";
import Card from "./layers/Card.vue";
import RangeIndicator from "./layers/RangeIndicator.vue";
import Timeline from "./layers/Timeline.vue";
import TextEditor from "./layers/TextEditor.vue";
import Menu from "./layers/Menu.vue";
import MenuItem from "./layers/MenuItem.vue";
import Cog from "./icons/Cog.vue";
import PenAndPaper from "./icons/PenAndPaper.vue";
import Database from "./icons/Database.vue";
import Box from "./icons/Box.vue";
import Letter from "./icons/Letter.vue";
import SlidingToggles from "./icons/SlidingToggles.vue";
import { getDaisyUiLink } from "../functions/getDaisyUiLink.js";
import FitText from "./layers/FitText.vue";

const range = ref(50);
const timelineHighlights = reactive({});
const fitTextHeight = ref(500);
const fitTextMax = ref(68);
const fitTextMin = ref(8);
const fontSize = ref(0);

const handleSettingsClick = () => {
  console.log("Clicked settings!");
};
</script>

<template>
  <main>
    <Card class="mb-4">
      <div class="text-2xl font-bold pb-2">Layered UI Composition Pattern</div>
      <div class="text-xl pb-2">Look at all the nice things we can make!</div>
      <span class="flex gap-1 align-items-center">
        <PenAndPaper></PenAndPaper>
        <a :href="getDaisyUiLink()">
          DaisyUI Template
        </a>
      </span>
      <div>TODO Make an FlowGridComponent</div>
    </Card>
    <div
      class="text-base-content mx-auto grid grid-cols-1 xs:grid-cols-1 gap-6 pb-20 sm:grid-cols-2 md:grid-cols-2 lg:grid-cols-3 [&>*]:mb-6">
      <div class="flex flex-col gap-4">
        <Card>
          <template #header class="flex items-center justify-between">
            <span class="flex items-center gap-2 font-semibold">
              <Cog></Cog> Form fields
            </span>
          </template>
          <!-- The props on the input layer are controlled, this is something to consider. You can also pass all
          attributes through to the underlying input, but maybe filter off classes, the point of the layer
          is to have strictness of layout. So be wary of that if the business logic requires passthrough. Maybe
          the classes that make the input look like its designed can be kept separate and the classes being passed
          through can be added on to the list of classes. -->
          <div class="pb-4">
            <PrimaryInput placeholder="Please enter your password" type="password">
              <!-- If you want to replace the default show/hide label, you do it with the #button named slot and just add whichever layers are needed for the new label -->
              <template #button="buttonProps">
                <!-- ScaleOnClick is a cool readable and lowly coupled way to add a simple or advanced animation and transition logic and styling to a component stack -->
                <ScaleOnClick>
                  <StrippedButton v-if="buttonProps.showPassword">🤫</StrippedButton>
                  <StrippedButton v-else>👁️</StrippedButton>
                </ScaleOnClick>
              </template>
            </PrimaryInput>
            <!-- The label can come from whatever reactive stuff controls the logic and payload of some form -->
            <ErrorLabel :textMessage="'some error message from the reactive form variable'">
            </ErrorLabel>
          </div>
          <div class="pb-4">
            <PrimaryInput placeholder="Please enter your email" type="text"></PrimaryInput>
            <ErrorLabel :textMessage="'some error message from the reactive form variable'">
            </ErrorLabel>
          </div>
          <button @click="console.log('submit')">
            <ScaleOnClick>
              <PrimaryButton>Submit</PrimaryButton>
            </ScaleOnClick>
          </button>
        </Card>
        <Card>
          <template #header>
            <PenAndPaper></PenAndPaper>
            Test of the FitText component
          </template>
          <Card>
            <template #header>Allowed height</template>
            Height ({{ Number(fitTextHeight) }}px)
            <RangeIndicator v-model="fitTextHeight" max="1000" min="50"></RangeIndicator>
            Min ({{ Number(fitTextMin) }}px)
            <RangeIndicator v-model="fitTextMin" max="100" min="8"></RangeIndicator>
            Max ({{ Number(fitTextMax) }}px)
            <RangeIndicator v-model="fitTextMax" max="100" min="8"></RangeIndicator>
          </Card>
          <FitText :style="{ height: fitTextHeight + 'px' }" @update:fontSize="fontSize = $event" :max="Number(fitTextMax)" :min="Number(fitTextMin)">
            <div class="text-l">This is a test title that we want to fit inside the square of this card</div>
          </FitText>
          <p class="text-sm text-gray-500 mt-1">
            Font size: {{ fontSize }}px
          </p>
          <div>Min: {{ fitTextMin }}px</div>
          <div>Max: {{ fitTextMax }}px</div>
        </Card>
      </div>
      <div class="flex flex-col gap-4">
        <Card>
          <h2 class="flex items-center justify-between"><span class="flex items-center gap-2 font-semibold">
              <Cog></Cog> Range indicator
            </span></h2>
          <div class="text-center text-5xl font-extralight">{{ range }}</div>
          <RangeIndicator v-model="range"></RangeIndicator>
        </Card>
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

        <Card>
          <template #header>
            <PenAndPaper></PenAndPaper>
            Write a new post
          </template>
          <TextEditor></TextEditor>
          <div class="card-actions grid grid-cols-2">
            <button class="btn">Draft</button>
            <button class="btn btn-primary">Publish</button>
          </div>
        </Card>
      </div>
      <div class="flex flex-col gap-4">
        <div class="card card-border border-base-300 bg-base-100">
          <Menu>
            <template #header>Menu panel</template>
            <a href="#" class="flex grow">
              <MenuItem>
              <Database></Database>
              <span class="grow">
                Databases
              </span>
              <span class="badge justify-self-end">7</span>
              </MenuItem>
            </a>
            <a href="#">
              <MenuItem>
              <Box></Box> Products
              </MenuItem>
            </a>
            <a href="#" class="flex grow">
              <MenuItem>
              <Letter></Letter>
              <span class="grow">Messages</span>
              <span class="badge justify-self-end">29</span>
              </MenuItem>
            </a>
            <button @click="handleSettingsClick">
              <MenuItem>
              <SlidingToggles></SlidingToggles>
              Settings
              </MenuItem>
            </button>
          </Menu>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
