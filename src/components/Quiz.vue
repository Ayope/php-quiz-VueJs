<template>
    <section class="quiz">
        <div class="header">
            <h1>PHP Quiz</h1>
        </div>
        
        <div class="quiz-info">
            <span class="question">{{ getCurrentQuestion.question }}</span>
            <span class="score">{{ score }} / {{ questions.length }}</span>
        </div>

        <div class="options">
            <label v-for="(option, index) in getCurrentQuestion.options"
            :key="index"
            :class="`option ${
                getCurrentQuestion.selected == index
                    ?index == getCurrentQuestion.answer
                        ? 'correct'
                        : 'wrong'
                    : ''
            }   ${
                getCurrentQuestion.selected != null &&
                index != getCurrentQuestion.selected
                    ?'disabled'
                    :''
            }`"
            >
            <input 
            type="radio"
            :name="getCurrentQuestion.index"
            :value="index"
            v-model="getCurrentQuestion.selected"
            :disabled="getCurrentQuestion.selected"
            @change="SetAnswer"
            >
            <span>{{ option }}</span>
            </label>
        </div>

        <!-- <button
            @click="NextQuestion"
            :disabled="!getCurrentQuestion.selected">
            {{ 
                getCurrentQuestion.index == questions.length - 1
                    ? 'Finish'
                :getCurrentQuestion.selected == null
                    ?'Select an option'
                    :'Next Question'
            }}
        </button> -->
        <button v-if="quizCompleted" @click="$emit('return-score',{score:score, questions:questions.length})">View Result</button>
        <button v-else @click="NextQuestion"  :disabled="!getCurrentQuestion.selected"> Next Question</button>
    </section>

    <!-- <section v-if="quizCompleted">
        <h3>You finished the quizzes</h3>
        <p>Your Score : {{ score }} / {{ questions.length }}</p>
    </section> -->
</template>

<script setup>
import {ref, computed} from 'vue'

const questions = ref([
    {
        question: 'What is Vue JS?',
        answer: 0,
        options: [
        'A front end framework',
        'A library',
        'An ice cream maker'
        ],
        selected: null
    },
    {
        question: 'What is Vuex?',
        answer: 2,
        options: [
        'Vue with an x',
        'A cheese selection',
        'State management library'
        ],
        selected: null
    },
    {
        question: 'What is Vue Router used for?',
        answer: 1,
        options: [
        'Walking in space',
        'A routing library for Vue JS',
        'Burger sauce',
        'Quzzes'
        ],
        selected: null
    }

]) 
const quizCompleted = ref(false)
const currentQuestion = ref(0)

const score = computed(()=>{
    let value = 0;
    questions.value.map(q => {
        if(q.selected == q.answer){
            value++;
        }
    })
    return value
})

const getCurrentQuestion = computed(()=>{
    let question = questions.value[currentQuestion.value];
    question.index = currentQuestion.value;
    return question
})

const SetAnswer = e =>{
    questions.value[currentQuestion.value].selected = e.target.value
    e.target.value = null
}

const NextQuestion = ()=>{
    if(currentQuestion.value < questions.value.length - 1){
        currentQuestion.value++;
    }else{
        quizCompleted.value =true;
    }
}


</script>

<style scoped>
    h1 {
        font-size: 2rem;
        margin-bottom: 2rem;
        color: black;
    }

    .quiz {
        background-color: gray;
        padding: 1rem;
        border-radius: 10px;
        text-align: center;
    }
    .quiz-info {
        display: flex;
        justify-content: space-between;
        margin-bottom: 1rem;
        color: black;
    }
    .quiz-info .question {
        font-size: 1.25rem;
    }
    .quiz-info.score {
        color: #FFF;
        font-size: 1.25rem;
    }
    .options {
        margin-bottom: 1rem;
    }
    .option {
        padding: 1rem;
        display: block;
        background-color: white;
        color: black;
        margin-bottom: 0.5rem;
        border-radius: 0.5rem;
        cursor: pointer;
    }
    .option:hover {
        background-color: black;
        color: white;
    }
    .option.correct {
        background-color: #2cce7d;
    }
    .option.wrong {
        background-color: #ff5a5f;
    }
    .option:last-of-type {
        margin-bottom: 0;
    }
    .option.disabled {
        opacity: 0.5;
    }
    .option input {
        display: none;
    }
    button {
        appearance: none;
        outline: none;
        border: none;
        cursor: pointer;
        padding: 0.5rem 1rem;
        background-color: #2cce7d;
        color: #2d213f;
        font-weight: 700;
        text-transform: uppercase;
        font-size: 1.2rem;
        border-radius: 0.5rem;
    }
    button:disabled {
        opacity: 0.5;
    }
    h2 {
        font-size: 2rem;
        margin-bottom: 2rem;
        text-align: center;
    }
    p {
        color: #8F8F8F;
        font-size: 1.5rem;
        text-align: center;
    }
</style>