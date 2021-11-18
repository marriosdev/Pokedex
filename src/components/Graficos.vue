<template>
    <div class="graficos">
        <p class="stat-name">{{ nome }}</p>
        <p class="quantidade">{{ tamanho }}</p>
        <div class="stat">
            <p class="barra-stat" :style="{width: `${tamanho}%`}">⠀⠀</p>
        </div>
        <p>100</p>
    </div>
</template>

<script>
export default {
    name: "Graficos",
    data() {
        return{
            // tamanho: null,
            // nome: null
        }
    },
    props: {
        tamanho: "",
        nome: ""
    }
}
</script>

<style scoped>
    .graficos{
        display: flex;
        padding: 10px;
        width: 300px;
    }
    .stat-name{
        width: 120px;
        text-transform: uppercase;
        font-size: 11pt;
    }
    .quantidade{
        width: 10%;
    }
    .stat{
        border: 1px solid #ff2b2b;
        margin: 4px;
        height: 15px;
        width: 200px;
    }
    .barra-stat{
        height: 100%;
        background: #ff1f1f;
    }
</style>
