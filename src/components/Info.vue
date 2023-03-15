<template>
    <section class="info">
        <h1>This is a php quiz</h1>
        <p>This is a php quiz for challenging your awareness in PHP</p>
        <button @click="showQuiz" class="BtnStartQuiz">Start the quiz</button>
    </section>
</template>

<script>
export default {
    methods:{
        showQuiz(){
            this.$emit('StartQuiz')
        }
    }
}
</script>

<style>

.info{
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

.BtnStartQuiz{
    border: none;
    border-radius: 10px;
    padding: 10px;
    cursor: pointer;
}

.BtnStartQuiz:hover{
    background-color: black;
    color: white;
}

</style>