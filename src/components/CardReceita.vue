<script lang="ts">
import type IReceitas from '../interfaces/IReceitas';
import { type PropType } from 'vue';

export default {
    props: {
        receita: { type: Object as PropType<IReceitas>, required: true}
    }
}
</script>

<template>
    <article class="card-receita">
        <header class="cabecalho-card">
            <img class="imagem-card" :src="`/imagens/receitas/${receita.imagem}`" alt="nome"  />
        </header>

        <div class="corpo-card">
            <p class="corpo-card__nome">
                {{ receita.nome }}
            </p>
        </div>
    </article>
</template>

<style scoped>
.card-receita {
    width: 17.625rem;
    max-width: 19.5rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    background: var(--Branco, #FFF);
    box-shadow: 4px 4px 12px 0px rgba(68, 68, 68, 0.08);
    border-radius: 1rem;
}

.imagem-card {
    width: 100%;
    border-radius: 1rem 1rem 0rem 0rem;
    display: block;
}

.corpo-card{
    padding: 2rem 1rem;
}

.corpo-card__nome{
    font-size: 22;
    font-weight: 600;
}
</style>
