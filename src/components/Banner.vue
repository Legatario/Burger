<template>
    <div class="main_burger">
        <h1>Make your Burguer</h1>
    </div>
</template>

<script>
    export default{
        name: "Banner"
    }
</script>

<style scoped>
    .main_burger{
        background-image: url('/img/burger.jpg');
        background-size: cover;
        background-position: 0 -250px;
        height: 800px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        background-repeat: no-repeat;
    }
    .main_burger h1{
        color: #fff;
        text-align: center;
        font-size: 60px;
        background: #222;
        padding: 20px;
    }
</style>