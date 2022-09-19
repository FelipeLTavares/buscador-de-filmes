<template>
  <div class="container-principal">
    <header>
        <h1>Buscador TVMaze</h1>
        <div class="buscador">
            <input type="text" class="buscar" v-model="busca">
            <button class="botao-busca" @click="getFilmes()">Procurar</button>
        </div>
    </header>
    <main>
        <CartaoFilme v-for="filme in listaFilmes"
        :key="filme.show.id" :filmeNome="filme.show.name" :filmeImagem="filme.show.image.original"
        :filmeUrl="filme.show.url" :filmeLingua="filme.show.language" :filmeGeneros="filme.show.genres"
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
                .then(e => {this.listaFilmes = e.data; console.log(e.data)});
        }
    },
    components: { CartaoFilme }
}
</script>


<style>
    .container-principal{
        display: grid;
        grid-template: 20vh auto 20vh/1fr 4fr;
        grid-template-areas: 'h h' 'm m' 'f f';
    }

    header{
        background-color: black;
        grid-area: h;
        display: grid;
        grid-template-columns: 1fr 2fr 1fr;
        align-items: center;
    }

    header > h1{
        font-size: 24px;
        color: white;
        margin: 10px;
    }

    .buscador{
        margin: 10px;
        height: 28px;
    }

    .buscador > input{
        height: 24px;
        min-width: 200px
    }

    .buscador > button{
        height: 30px;
        font-weight: 600;
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
        justify-items: center;
    }
    footer{
        grid-area: f;
        background-color: black;
    }

    @media (max-width: 1008px){
        .container-principal{
            grid-template: 20vh 15vh auto 20vh/1fr 4fr;
            grid-template-areas: 'h h' 'm m' 'm m' 'f f';
        }
        main{
            grid-template-columns: auto auto;
        }
        header{
            grid-template-columns: auto auto;
        }
    }
    
    @media (max-width: 770px){
        header{
            grid-template-columns: auto;
            gap: 0px;
            align-items: center;
        }
        main{
            min-height: 70vh;
            grid-template-columns: auto auto;
        }
    }

    @media(max-width: 480px){
        main{
            grid-template-columns: auto;
        }
    }

</style>