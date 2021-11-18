<template>
    <div>
        <h1>Pokédex</h1>
        <a href="https://github.com/edmariooliver" target="_blank">
            <img src="https://cdn-icons-png.flaticon.com/512/25/25231.png" alt="">
        </a>
    </div>
</template>

<script>
    export default {
        name: "Navbar",
        data() {
            return {
                teste: "teste"
            }
        }
    }
</script>

<style scoped>
    h1{
        align-self:center;
    }
    img{
        height: 30px;
    }
    div{
        justify-content: space-around;
        display: flex;
        color: white;
        background: #f82424;
        padding: 10px;
        margin-bottom: 20px;
        text-align: center;
    }
</style>