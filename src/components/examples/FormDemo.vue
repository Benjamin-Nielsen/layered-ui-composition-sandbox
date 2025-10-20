<script setup>
import Cog from '../icons/Cog.vue';
import PrimaryButton from '../layers/forms/PrimaryButton.vue';
import PrimaryInput from '../layers/forms/PrimaryInput.vue';
import StrippedButton from '../layers/forms/StrippedButton.vue';
import ScaleOnClick from '../layers/animations/ScaleOnClick.vue';
import ErrorLabel from '../layers/forms/ErrorLabel.vue';
import Card from '../layers/buildingBlocks/Card.vue';

</script>
<template>
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
</template>