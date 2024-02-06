<template>
    <div class="tasks">
        <Task @toggle-reminder="$emit('toggle-reminder', task.id)"  v-for="task in tasks" :key="task.id" :task="task" @delete="$emit('delete', task.id)"/>
    </div>
</template>

<script>
import Task from './Task.vue'

export default {
    props:{
        tasks : Array
    },
    components:{
        Task
    },
    emits:['delete','toggle-reminder']
}
</script>

<style>

</style>