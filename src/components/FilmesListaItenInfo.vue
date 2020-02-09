<template>
    <div>
        <h2> Filmes Selecionados </h2>
        <div class="card">
            <div v-if="filme" class="card-body">
                <h5 class="card-title">{{ filme.titulo }}</h5>
                <button @click="editarFilme" class="btn btn-danger float-right">Editar</button>
            </div>
            <div v-else class="card-body">
                <h5 class="card-title">Nenhum filmes Selecionado</h5>
            </div>
        </div>
    </div>
</template>

<script>

import {eventBus} from './../main'

export default {
    data(){
        return {
            filme: undefined
        }
    },
    methods: {
        editarFilme(){
            this.$emit("editarFilme", this.filme)
        }
    },
    created(){
        eventBus.$on("filmeSelecionado", (filmeSelecionado) => {
            this.filme = filmeSelecionado
        })
    }
}
</script>