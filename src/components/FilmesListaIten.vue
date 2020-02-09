<template>
    <li class="list-group-item" >
        {{ filme.titulo }} | {{ filme.ano }}
        <button v-if="filme" @click="selecionarFilme" class="btn btn-secondary float-right">Selecionar</button>
    </li>
</template>

<script>

import {eventBus} from './../main';

export default {
   props: {
       filme: {
           type: Object,
           required: true
       }
   }, 
   methods: {
       selecionarFilme(){
        eventBus.$emit("filmeSelecionado", this.filme);
       }
   }
}
</script>