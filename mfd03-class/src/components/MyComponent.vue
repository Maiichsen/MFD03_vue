<script setup> 
import { ref } from "vue"; //ref er en refremnce til vores datamodel

const message = ref('hello vue 3.0'); // Når der er message på er det en twoWay binding
</script>

<template>
    <div>
        <h1>MyComponet</h1>
        <p>{{ message }}</p>
        <input v-model="message">
    </div>
</template>

<style scoped lang="scss"></style>

