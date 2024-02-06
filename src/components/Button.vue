<template>
  <button class="btn" :class="['btn-' + color, addClass]" @click="$emit('btn-clicked')">{{ content }}</button>
</template>

<script>
export default {
    name: 'Button',
    props:{
        color : {
            type:String,
            default : "dark"
        },
        content : String,
        addClass:{
            type:String,
        }
    }
}
</script>

<style>

</style>