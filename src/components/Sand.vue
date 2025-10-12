<script setup>
import PrimaryInput from "./layers/PrimaryInput.vue";
import ErrorLabel from "./layers/ErrorLabel.vue";
import ScaleOnClick from "./layers/ScaleOnClick.vue";
import StrippedButton from "./layers/StrippedButton.vue";
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
    <!-- The props on the input layer are controlled, this is something to consider. You can also pass all
     attributes through to the underlying input, but maybe filter off classes, the point of the layer
     is to have strictness of layout. So be wary of that if the business logic requires passthrough. Maybe
     the classes that make the input look like its designed can be kept separate and the classes being passed
     through can be added on to the list of classes. -->
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
    <ErrorLabel
      :textMessage="'some error message from the reactive form variable'"
    >
    </ErrorLabel>
    <PrimaryInput
      placeholder="Please enter your email"
      type="text"
    ></PrimaryInput>
    <ErrorLabel
      :textMessage="'some error message from the reactive form variable'"
    >
    </ErrorLabel>
  </main>
</template>

<style scoped></style>
