<template>
  <form @submit.prevent="HandleForm">
    <div class="inputs">
        <label for="Task">Task:</label>
        <input v-model="Task" required type="text" name="Task" id="Task" placeholder="(e.g. Learning a new FrameWork)">
    </div>
    <div class="inputs">
        <label for="Time">Date & Time:</label>
        <input v-model="Time" required type="text" name="time" id="Time" placeholder="(e.g. March 1st 2022 - 11:00am)">
    </div>
    <div class="inputs check">
        <label for="reminder">Set Reminder:</label>
        <input v-model="reminder" type="checkbox" name="reminder" id="reminder" value="true">
    </div>
    <div class="btnDiv">
        <Button color="success"  content="Save Task"/>
    </div>
  </form>
</template>

<script setup>
import {ref, defineEmits  } from 'vue';
import Button from '../Button.vue'


let emit = defineEmits(['saveTask'])
const Task = ref('') 
const Time = ref('')
const reminder = ref(false)

const HandleForm = (e)=>{
    if(Task == ""|| Time == ""){
        alert("Please fill all the fields")
        return
    }
    
    emit('saveTask',{Task:Task.value, Time: Time.value, reminder:reminder.value})

    document.querySelector('form').reset()
}

</script>

<style scoped>
    .inputs{
        width:100%;
        margin:1rem auto;
    }
    input{
        display: block;
        width:100%;
        padding:4px;
    }
    label{
        font-size:1.1rem;
    }
    .check{
        display: flex;
        justify-content: flex-start;
        align-items: center;
        gap:1rem;
    }
    .check input {
        width:min-content
    }
    .btnDiv{
        margin-top:1.5rem;
        display: flex;
        justify-content: center;
    }
</style>