<script setup>
import { ref } from "vue";
const isEditable = ref(false);
</script>

<template>
    {{ isEditable }}
<button @click="isEditable = !isEditable">
    {{ isEditable ? 'Gør ikke redigerbar' : 'Gør redigerbar' }}
    </button>
<p :contenteditable="isEditable">Dette er en tekst, som du kan redigere</p>
<div v-if="isEditable">Kan vises hvis true</div>
</template>

<style scoped lang="scss">
</style>