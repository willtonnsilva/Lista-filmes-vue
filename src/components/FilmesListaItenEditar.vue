<template>
    <div>
        <h2>Editar filme</h2>

        <div class="form-group">
            <label>Título:</label>
            <input type="text" 
                class="form-control" 
                placeholder="Insira o título"
                :value="filmeSelecionado.titulo"
                @input="filmeSelecionado = { propriedade: 'titulo', valor: $event.target.value}"
            />
        </div>

        <div class="form-group">
            <label>Ano:</label>
            <input type="text" 
                class="form-control" 
                placeholder="Insira o Ano"
                :value="filmeSelecionado.ano"
                @input="filmeSelecionado = { propriedade: 'ano', valor: $event.target.value, id: filmeSelecionado.id}"
            />
        </div>

        <div class="form-group text-right" >
            <button @click="atualizaFilme" type="button" class="btn btn-primary">Salvar</button>
        </div>
        
    </div>
</template>

<script>

import {eventBus} from './../main'

export default {
    props: {
        filme: {
            type: Object,
            required: true
        }
    },
    data(){
        return {
            filmeLocal: this.filme
        }
    },
    computed: {
        filmeSelecionado: {
            set(dado){
                this.filmeLocal = Object.assign(
                    {},
                    this.filmeLocal,
                    { [ dado.propriedade ] : dado.valor, id: this.filmeSelecionado.id },
                )
            },
            get(){
                return this.filme 
            }
        }
    },
    methods: {
        atualizaFilme(){
            eventBus.$emit("filmeAtualizacao", this.filmeLocal)
        }
    }
}
</script>