<template>
    <header>
        <h1> {{ title }} </h1>
        <Button @btn-clicked="$emit('toggle-add-task')" :content="currentButtonContent" :color="currentButtonColor"/>
    </header>
</template>

<script>
import Button from './Button.vue'

export default {
    name: 'Header',
    props:{
        title: String,
        currentButtonContent: String, 
        currentButtonColor: String
    },
    components:{
        Button
    }
}
</script>

<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    h1 {
        font-size : 2rem ;
    }
    @media screen and (max-width: 350px) {
        header{
            flex-direction: column;
            align-items: flex-start;
        }
    }
</style>