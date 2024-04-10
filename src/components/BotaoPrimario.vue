<script lang="ts">
    export default {
        props: {
            texto:  { type: String, required: true }
        }
    }
</script>


<template>
    <button class="botao-principal">
        {{ texto }}
    </button>
</template>

<style scoped>
    .botao-principal{
        width: 312px;
        height: 56px;
        background-color: var(--coral);
        color: var(--creme);
        border-radius: 32px;
        font-size: 22px;
        font-weight: bold;
        cursor: pointer;
    }

    .botao-principal:hover{
        background-color: var(--ocre);
    }
</style>