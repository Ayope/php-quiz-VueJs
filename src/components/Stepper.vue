<template>
    <div class="container">
      <div :class="
        state.state == 'info'
        ?'active'
        :'step'
      ">info</div>
      <div  :class="
        state.state == 'quiz'
        ?'active'
        :'step'
      ">Quiz</div>
      <div :class="
        state.state == 'score'
        ?'active'
        :'step'
      ">Score</div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue'

const state = defineProps(['state'])

</script>

<style>
    .container{
        display: flex;
        justify-content: space-around;
    }
    .container > div{
        padding: 1%;
        border: black 2px solid;
        border-radius: 50%;
        width: 25px; /* adjust this to the desired size */
        height: 25px; /* adjust this to the desired size */
        /* text-align: center; */
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .container > div:hover{
        background-color: black;
        color: white;
    }
    .active{
        background-color: green;
    }
    .step{
        background-color: white;
        color: black;
    }
</style>