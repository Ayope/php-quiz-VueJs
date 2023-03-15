<template>
    <section class="score">
        <h3>You finished the quiz</h3>
        <p>Your Score : {{ result.result.score }} / {{ result.result.questions }}</p>
    </section>
</template>


<script setup>
import { defineProps } from 'vue';

const result = defineProps(['result'])

</script>

<style scoped>
    h3{
        font-size: 2rem;
        margin-bottom: 2rem;
        color: black;
    }
    p{
        font-size: 1.5rem;
    }
    section{
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        flex-direction: column;
        padding: 10%;
        border-radius: 10px;
        background-color: gray;
        border: none;
    }
</style>