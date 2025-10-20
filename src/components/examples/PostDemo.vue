<script setup>
import PenAndPaper from '../icons/PenAndPaper.vue';
import TextEditor from '../layers/buildingBlocks/TextEditor.vue';
import Card from '../layers/buildingBlocks/Card.vue';
</script>
<template>
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
</template>