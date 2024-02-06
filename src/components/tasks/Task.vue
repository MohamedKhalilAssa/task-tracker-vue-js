<template>
  <div @click="$emit('toggle-reminder', task.id)" :class="[ task.reminder ? 'reminder' : '', 'task']">
    <h2> {{task.text}} <i @click="$emit('delete', task.id)" class="close fas fa-times"></i></h2>
    <h6> {{task.day}} </h6>
  </div>
</template>

<script>
export default {
    props:{
        task : Object
    }
}
</script>

<style scoped>
    .task{
        background: #eee;
        padding:0.7rem;
        margin-top:1rem;
        border-radius:0 12px 12px 0;
        position: relative;
    }
    .task.reminder {
        border-left: 5px solid red;
    }
    .close{
        cursor: pointer;
        color:red;
        position: absolute;
        top:6px;
        right:16px;
    }
</style>