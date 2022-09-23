<template>
  <div class="container-principal">
    <header ref="head">
        <h1>Buscador TVMaze</h1>
        <div class="buscador">
            <input type="text" class="buscar" v-model="busca" placeholder="Pesquise aqui..." @keyup.enter="getFilmes()">
            <button class="botao-busca" @click="getFilmes()">Procurar</button>
        </div>
    </header>
    <main v-if="vazio">
        <CartaoFilme v-for="filme in listaFilmes"
        :key="filme.id" :filmeNome="filme.name" :filmeImagem="filme.image.medium"
        :filmeUrl="filme.url" :filmeLingua="filme.language" :filmeGeneros="filme.genres"
        />
    </main>
    <main v-else class="mensagem"> {{mensagem}} </main>
    <footer @click="voltarTopo()"><h4>Clique aqui para voltar para o topo!</h4></footer>
  </div>
</template>

<script>
import axios from 'axios'
import CartaoFilme from '../components/cartao-filme.vue'

export default {
    name: "filmes-view",
    data() {
        return {
            listaFilmes: [],
            busca: "",
            mensagem: 'Procure por filmes e séries aqui!',
            vazio: false
        };
    },
    methods: {
        async getFilmes() {
            await axios.get("https://api.tvmaze.com/search/shows?q=" + this.busca)
                .then(e => {
                        let listaProvisoria1 = e.data;
                        let listaProvisoria2 = [];
                        for (let filme of listaProvisoria1){
                            if(filme.show.image == null){
                                continue
                            }
                            listaProvisoria2.push(filme.show)
                        }
                        listaProvisoria2.length == 0? this.vazio = false: this.vazio = true;
                        this.listaFilmes = listaProvisoria2;
                        this.mensagem = 'Sem resultado para esta pesquisa... 😢';
                });
        },

        voltarTopo(){
            this.$refs['head'].scrollIntoView({behavior: "smooth"})
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
        background-color: #1C1C1C	;
        grid-area: h;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    header > h1{
        font-size: 30px;
        color: white;
        margin-left: 20px;
    }
    .buscador{
        height: 28px;
        margin: 20px;
    }
    .buscador > input{
        font-family: 'Rajdhani', sans-serif;
        height: 24px;
        min-width: 200px;
        border-radius: 5px 0 0 5px;
        padding-left: 8px;
    }
    .buscador > button{
        font-family: 'Rajdhani', sans-serif;
        height: 32px;
        font-weight: 600;
        border-radius: 0 5px 5px 0;
    }
    main{
        grid-area: m;
        display: grid;
        min-height: 60vh;
        grid-template-columns: auto auto auto;
        gap: 10px;
        justify-items: center;
    }
    .mensagem{
        display: grid;
        align-items: center;
        justify-content: center;
    }
    footer{
        grid-area: f;
        background-color: #1C1C1C;
        display: grid;
        align-items: center;
        justify-content: center;
        color: white;
    }
    footer > h4:hover{
        cursor: pointer;
    }

    @media (max-width: 1008px){
        .container-principal{
            grid-template: 15vh auto 20vh/1fr 4fr;
            grid-template-areas: 'h h' 'm m' 'f f';
        }
        main{
            min-height: 65vh;
            grid-template-columns: auto auto;
        }
    }
    
    @media (max-width: 770px){
        .container-principal{
            grid-template: 20vh auto 20vh/1fr 4fr;
            grid-template-areas: 'h h' 'm m' 'f f';
        }
        main{
            min-height: 60vh;
        }
        header > h1{
            font-size: 24px;
            color: white;
        }
    }

    @media(max-width: 610px){
        main{
            grid-template-columns: auto;
        }
        header{
            flex-direction: column;
            align-items: center;
            justify-content: space-evenly;
            padding: 0;
        }
        header > h1{
            margin: 0;
        }
        header > .buscador{
            margin: 0;
        }
    }
</style>