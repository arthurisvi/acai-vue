<template>
    <div id ="main-banner">
        <h1>Monte seu Açaí</h1>
    </div>

</template>

<script>
export default{
    name: 'Banner'
}

</script>

<style scoped>
    #main-banner{
        background-image: url('/img/acai.png');
        background-size: cover;
        background-position: 0;
        height: 650px;
        display: flex;
        align-items: center;
        justify-content: flex-end;

    }

    #main-banner h1{
        color: #FFF;
        font-size: 60px;
        text-align: center;
        padding: 20px 40px;
        background-color: #4C2D51
    }

</style>