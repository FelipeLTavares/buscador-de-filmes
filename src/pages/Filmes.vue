<template>
  <div class="container-principal">
    <header>
        <input type="text" class="buscar" v-model="busca">
        <button class="botao-busca" @click="getFilmes()">Procurar</button>
    </header>
    <aside></aside>
    <main>
        <CartaoFilme v-for="filme in listaFilmes"
        :key="filme.show.id" :filmeNome="filme.show.name" :filmeDescricao="filme.show.summary" :filmeUrl="filme.show.image.original"
        />
    </main>
    <footer></footer>
  </div>
</template>

<script>
import axios from 'axios'
import CartaoFilme from '../components/cartao-filme.vue'

export default {
    name: "filmes-view",
    data() {
        return {
            listaFilmes: "",
            busca: ""
        };
    },
    methods: {
        async getFilmes() {
            await axios.get("https://api.tvmaze.com/search/shows?q=" + this.busca)
                .then(e => this.listaFilmes = e.data);
        }
    },
    components: { CartaoFilme }
}
</script>


<style>
    .container-principal{
        display: grid;
        grid-template: auto auto auto/1fr 4fr;
        grid-template-areas: 'h h' 'a m' 'f f';
    }

    header{
        background-color: black;
        grid-area: h;
        height: 50px;
    }

    aside{
        grid-area: a;
        background-color: gray;
    }
    main{
        grid-area: m;
        display: grid;
        min-height: 550px;
        grid-template-columns: auto auto auto;
        gap: 10px;
        justify-content: auto;
    }
    footer{
        grid-area: f;
        background-color: black;
        height: 100px;
    }
    .teste{
        width: 300px;
        height: 150px;
        background-color: red;
        margin: auto;
    }    
</style>