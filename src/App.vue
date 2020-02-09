<template>
    <div>
        <div class="jumbotron jumbotron-fluid">
            <div class="container">
                <h1 class="display-2">Lista de Filmes</h1>
                <p class="lead"> Treinando comunicação entre components no Vue. </p>
            </div>
        </div>
        <div class="container">
            <FilmesLista/>
        </div>
    </div>
</template>

<script>

import FilmesLista from './components/FilmesLista.vue'

export default {
    components: {
        FilmesLista
    }
}
</script>