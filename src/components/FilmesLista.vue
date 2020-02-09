<template>
    <div class="row">
        <div class="col-8">
            <h2> Filmes </h2>
            <ul class="list-group list-group-flush">
                <FilmesListaItens 
                v-for="filme in listaFilmes"
                :key="filme.id"
                :filme="filme"
                :class="aplicaClasseActiva(filme)"
                @filmeEscolhido="filmeSelecionado = $event"
            />
            </ul>
        </div>
         <div class="col-4">
            <FilmesListaInfo
                v-if="!editar"
                :filmeSelecionado="filmeSelecionado"
                @editarFilme="editarFilme"
            />

            <FilmesListaItenEditar 
                v-else
                :filme="filmeSelecionado"
            />
        </div> 
    </div>
</template>

<script>

import FilmesListaItens from './FilmesListaIten'
import FilmesListaItenEditar from './FilmesListaItenEditar'
import FilmesListaInfo from './FilmesListaItenInfo'
import {eventBus} from './../main'

export default {
    components: {
        FilmesListaItens,
        FilmesListaItenEditar,
        FilmesListaInfo
    },
    data(){
        return {
            listaFilmes : [
                {
                    id: 1,
                    titulo: "Vigandores Ultimato",
                    ano: 2018
                },
                {
                    id: 2,
                    titulo: "Minha mãe é uma peça 3",
                    ano: 2020
                },
                {
                    id: 3,
                    titulo: "Capitan Marvel",
                    ano: 2019
                },
                {
                    id: 4,
                    titulo: "Joker",
                    ano: 2019
                }
            ],
            filmeSelecionado: undefined,
            editar: false
        }
    },
    methods: {
        aplicaClasseActiva(filmeItem){
            return {
                active: this.filmeSelecionado && this.filmeSelecionado.id === filmeItem.id
            }
        },
        editarFilme(){
            this.editar = true;
        },
        atualizarFilme(filmeAtualizado){
            const indice = this.listaFilmes.findIndex(filme => filme.id === filmeAtualizado.id);
            this.listaFilmes.splice(indice, 1, filmeAtualizado);
            this.editar = false;
            this.filmeSelecionado = undefined;
        }
    },
    created(){
        eventBus.$on("filmeSelecionado", (filme) => {
            this.filmeSelecionado = filme
        });

        eventBus.$on("filmeAtualizacao", this.atualizarFilme)
    }
}
</script>