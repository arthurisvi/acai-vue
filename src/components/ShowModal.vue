<template>
    <div class = "input-container">
        <input @click="$emit('showModal')" type ="submit" class = "submit-btn" value="Montar açaí">
    </div> 
</template>

<script>
    export default{
        name: 'ShowModal',
        emits: 'showModal'
    }

</script>

<style scoped>
.submit-btn{
        background-color: #4C2D51;
        color: #fff;
        font-weight: bold;
        border: 2px solid #4C2D51;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: 0.5s;
        width: 300px;
    }

    .submit-btn:hover{
        background-color: transparent;
        color: rgb(132, 181, 28, 1);
    }

</style>