<template>
  <main class="main border border-black">
    <Header @toggle-add-task="CurrentlySavingTask=!CurrentlySavingTask"  title="Task Tracker" :currentButtonContent="CurrentlySavingTask? 'Close':'Add Task'" 
    :currentButtonColor="CurrentlySavingTask ? 'danger' : 'dark'"/>
    <addTask @saveTask="saveTaskHandling"  v-if ="CurrentlySavingTask"/>
    <Tasks @toggle-reminder="toggleReminder" @delete="deleteTask" :tasks="TasksArr"/>
  </main>
</template>

<script setup>
  import { ref,defineEmits } from 'vue'
  import Header from './components/Header.vue'
  import Tasks from './components/tasks/Tasks.vue'
  import addTask from './components/tasks/AddTask.vue'


  let CurrentlySavingTask = ref(false)

  // adding mock tasks for reference
  let TasksArr = ref([])


// Loading already saved tasks 
const loading = ()=>{
  TasksArr.value = localStorage.getItem("savedTasks") ?  JSON.parse(localStorage.getItem("savedTasks")) : []
}
// calling the function
loading()

//toggle reminder on  click
  const toggleReminder = (id) =>{
    TasksArr.value.forEach((task)=>{
      if (task.id === id){
        task.reminder = !task.reminder
         // Push the changes into localStorage
        localStorage.setItem('savedTasks', JSON.stringify(TasksArr.value))
        return
      }
    })
  }
  //delete the necessary task
  const deleteTask = (id) =>{
    if(confirm("Are you sure you want to delete this task?")){
        TasksArr.value = TasksArr.value.filter((task)=>{
        return task.id !== id
      })
      // Push the changes into localStorage
      localStorage.setItem('savedTasks', JSON.stringify(TasksArr.value))
    }
  }

  // add another task
  const saveTaskHandling = ({Task, Time, reminder})=>{
    const newTask = {
      id : TasksArr.value.length + 1,
      text : Task,
      day : Time,
      reminder : reminder
    } 
    TasksArr.value.push(newTask)

    // Pushing the tasksArray to Local Storage
    localStorage.setItem('savedTasks', JSON.stringify(TasksArr.value))
  }

</script>

<style>

.main{
  padding:1rem;
  width:98%;
  min-height: 10vh;
  max-width: 750px;
  margin: 0 auto;
  border-radius:12px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap:1rem;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  min-height:100vh;
}
</style>
