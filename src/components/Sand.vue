<script setup>
import PrimaryInput from "./layers/PrimaryInput.vue";
import ErrorLabel from "./layers/ErrorLabel.vue";
import ScaleOnClick from "./layers/ScaleOnClick.vue";
import StrippedButton from "./layers/StrippedButton.vue";
import PrimaryButton from "./layers/PrimaryButton.vue";
import Card from "./layers/Card.vue";
</script>

<template>
  <main>
    <div class="text-2xl font-bold pb-2">Inputs</div>
    <div class="pb-2">
      The Input layer had to be designed a bit different than the first layers
      of the other form components because the input html element is a self
      closing element. Meaning that the outmost layer can not become the input
      element itself like with the other form components like buttons for
      example. But the way it's developed here it seems to have the same
      benefits of layered composition as the other ones so no biggie.
    </div>
    <div class="pb-5">
      TODO We need some way to pass validation rules to the input, or maybe a
      validation system that doesn't live in the input layer. Since the error
      label doesn't have to live here, and the validation logic would be
      completely dynamic and given from the outside, maybe it shouldn't be the
      responsibility of this layer to orchestrate it.
    </div>
    <div class="pb-5">
      TODO Whatever reactive variable the input is bound to, needs to be able to
      passthrough from the composing component.
    </div>
    <div class="text-base-content mx-auto grid gap-6 pb-20 sm:grid-cols-2 md:grid-cols-1 lg:grid-cols-2 [&>*]:mb-6">
      <div class="flex flex-col gap-4">
        <Card>
          <h2 class="flex items-center justify-between"><span class="flex items-center gap-2 font-semibold"><svg
                xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                stroke="currentColor" class="size-5 opacity-40">
                <path stroke-linecap="round" stroke-linejoin="round"
                  d="M9.594 3.94c.09-.542.56-.94 1.11-.94h2.593c.55 0 1.02.398 1.11.94l.213 1.281c.063.374.313.686.645.87.074.04.147.083.22.127.325.196.72.257 1.075.124l1.217-.456a1.125 1.125 0 0 1 1.37.49l1.296 2.247a1.125 1.125 0 0 1-.26 1.431l-1.003.827c-.293.241-.438.613-.43.992a7.723 7.723 0 0 1 0 .255c-.008.378.137.75.43.991l1.004.827c.424.35.534.955.26 1.43l-1.298 2.247a1.125 1.125 0 0 1-1.369.491l-1.217-.456c-.355-.133-.75-.072-1.076.124a6.47 6.47 0 0 1-.22.128c-.331.183-.581.495-.644.869l-.213 1.281c-.09.543-.56.94-1.11.94h-2.594c-.55 0-1.019-.398-1.11-.94l-.213-1.281c-.062-.374-.312-.686-.644-.87a6.52 6.52 0 0 1-.22-.127c-.325-.196-.72-.257-1.076-.124l-1.217.456a1.125 1.125 0 0 1-1.369-.49l-1.297-2.247a1.125 1.125 0 0 1 .26-1.431l1.004-.827c.292-.24.437-.613.43-.991a6.932 6.932 0 0 1 0-.255c.007-.38-.138-.751-.43-.992l-1.004-.827a1.125 1.125 0 0 1-.26-1.43l1.297-2.247a1.125 1.125 0 0 1 1.37-.491l1.216.456c.356.133.751.072 1.076-.124.072-.044.146-.086.22-.128.332-.183.582-.495.644-.869l.214-1.28Z">
                </path>
                <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z"></path>
              </svg> Form fields</span></h2>
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
      </div>
      <div class="flex flex-col gap-4">
        <Card>
          <h2 class="flex items-center justify-between"><span class="flex items-center gap-2 font-semibold"><svg
                xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                stroke="currentColor" class="size-5 opacity-40">
                <path stroke-linecap="round" stroke-linejoin="round"
                  d="M9.594 3.94c.09-.542.56-.94 1.11-.94h2.593c.55 0 1.02.398 1.11.94l.213 1.281c.063.374.313.686.645.87.074.04.147.083.22.127.325.196.72.257 1.075.124l1.217-.456a1.125 1.125 0 0 1 1.37.49l1.296 2.247a1.125 1.125 0 0 1-.26 1.431l-1.003.827c-.293.241-.438.613-.43.992a7.723 7.723 0 0 1 0 .255c-.008.378.137.75.43.991l1.004.827c.424.35.534.955.26 1.43l-1.298 2.247a1.125 1.125 0 0 1-1.369.491l-1.217-.456c-.355-.133-.75-.072-1.076.124a6.47 6.47 0 0 1-.22.128c-.331.183-.581.495-.644.869l-.213 1.281c-.09.543-.56.94-1.11.94h-2.594c-.55 0-1.019-.398-1.11-.94l-.213-1.281c-.062-.374-.312-.686-.644-.87a6.52 6.52 0 0 1-.22-.127c-.325-.196-.72-.257-1.076-.124l-1.217.456a1.125 1.125 0 0 1-1.369-.49l-1.297-2.247a1.125 1.125 0 0 1 .26-1.431l1.004-.827c.292-.24.437-.613.43-.991a6.932 6.932 0 0 1 0-.255c.007-.38-.138-.751-.43-.992l-1.004-.827a1.125 1.125 0 0 1-.26-1.43l1.297-2.247a1.125 1.125 0 0 1 1.37-.491l1.216.456c.356.133.751.072 1.076-.124.072-.044.146-.086.22-.128.332-.183.582-.495.644-.869l.214-1.28Z">
                </path>
                <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z"></path>
              </svg> Range indicator</span></h2>
          <div class="text-center text-5xl font-extralight">27</div>
          <input type="range" class="range range-sm w-full">
        </Card>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
