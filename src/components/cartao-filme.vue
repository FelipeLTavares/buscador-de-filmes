<template>
  <div class="container-filme">
    <a :href="filmeUrl"><img :src="filmeImagem" :alt="filmeNome"/></a>
    
    <div class="containerInfo">
      <h3>{{filmeNome}}</h3>
      <p> Gênero(s): {{filmeStringGenero}}</p>
      <p>Linguagem: {{filmeLingua}}</p>
    </div>
  </div>
</template>

<script>
export default {
    name: 'cartao-filme',
    props: {
      filmeImagem: String,
      filmeNome: String,
      filmeUrl: String,
      filmeLingua: String,
      filmeGeneros: Array
    },
    data() {
      return {
        filmeStringGenero: '',
      }
    },
    methods: {
        tratarGeneros(){
          if(this.filmeGeneros.length<1){
            this.filmeStringGenero = 'Indefinido'
          } else {
            this.filmeStringGenero = this.filmeGeneros.join(', ')
          }
        }
      },
    mounted(){
      this.tratarGeneros()
    }
  }
</script>

<style>
.container-filme{
  box-sizing: border-box;
  background-color: #282828;
  border-radius: 5px;
  box-shadow: 2px 2px 2px 2px black;
  width: 280px;
  max-height: 150px;
  display: flex;
  justify-content: space-between;
  margin: 8px;
}
img{
  max-height: 150px;
  border-radius: 5px;
  margin-left: 0;
}
.containerInfo{
  text-align: left;
  width: 150px;
  color: white
}
.containerInfo>h3{
  font-size: 16px;
  font-weight: 600;
}
.containerInfo>p{
  font-size: 13px;
}
</style>