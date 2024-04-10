<script lang="ts">
import { obterReceitas } from '@/http';
import type IReceitas from '../interfaces/IReceitas';
import CardReceita from './CardReceita.vue';
import BotaoPrimario from './BotaoPrimario.vue';
import { type PropType } from 'vue';
import { itemDeLista1EstaoEmLista2 } from '@/operacoes/listas';

export default {
    props:{
        ingredientes: { type: Array as PropType<string[]>, required: true }
    },
    data() {
        return {
            receitasEncontradas: [] as IReceitas[]
        }
    },
    async created() {
        const receitas = await obterReceitas();

        this.receitasEncontradas = receitas.filter((receita) => {
            const receitaPossivel = itemDeLista1EstaoEmLista2(receita.ingredientes, this.ingredientes)

            return receitaPossivel
        })
    },
    components: { CardReceita, BotaoPrimario },
    emits: ['editarLista']
}
</script>

<template>
    <section class="mostrar-receitas">
        <h1 class="cabecalho titulo-receitas">Receitas</h1>
        <p class="paragrafo-lg resultados-encontrados">Resultados encontrados: {{ receitasEncontradas.length }}</p>

        <div v-if="receitasEncontradas.length" class="receitas-encontradas">
            <p class="paragrafo-lg informacoes">
                Veja as opções de receitas que encontramos com os ingredientes que você tem por aí!
            </p>

            <ul class="receitas">
                <li v-for="receita of receitasEncontradas" :key="receita.nome">
                    <CardReceita :receita="receita" />
                </li>
            </ul>
        </div>

        <div v-else class="receitas-nao-encontradas">
            <p class="paragrafo-lg receitas-nao-encontradas__info">
                Ops, não encontramos resultados para sua combinação. Vamos tentar de novo?
            </p>
            <img src="../assets/images/sem-receitas.png">
            
        </div>
        <BotaoPrimario texto="Editar lista" @click="$emit('editarLista')" />
    </section>
</template>

<style scoped>
.mostrar-receitas {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.resultados-encontrados {
    color: var(--verde-medio);
    margin-bottom: 1.5rem;
}

.titulo-receitas {
    color: var(--verde-medio);
    margin-bottom: 1.5rem;
}

.informacoes {
  margin-bottom: 2rem;
}

.receitas{
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
    margin-bottom: 2rem;
}

.receitas-nao-encontradas {
    margin-bottom: 2rem;
}

.receitas-nao-encontradas__info {
    margin-bottom: 0.5rem;
}
</style>