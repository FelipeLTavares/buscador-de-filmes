<template>
  <div class="container-filme">
    <img :src="filmeUrl" :alt="filmeNome">
    <div class="containerInfo">
      <h3>{{filmeNome}}</h3>
      <p>{{filmeSinopse}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'cartao-filme',
  props: {
    filmeUrl: String,
    filmeNome: String,
    filmeDescricao: String
  },
  data() {
    return {
      filmeSinopse: this.filmeDescricao
    }
  },
  methods: {
    verificarSinopse(){
      if (this.filmeDescricao.length > 100){
        this.filmeSinopse = this.filmeDescricao.slice(0,120) + '...'
      } 
    }
  },
  mounted(){
    this.verificarSinopse()
  }
}
</script>

<style>
.container-filme{
  box-sizing: border-box;
  border: 1px solid gray;
  border-radius: 5px;
  max-width: 300px;
  max-height: 150px;
  display: grid;
  grid-template-columns: 2fr 3fr;
  margin: 10px;
}
img{
  max-height: 150px;
  border-radius: 5px;
}
.containerInfo{
  text-align: left;
}
.containerInfo>h3{
  font-size: 14px;
  font-weight: 600;
}
.containerInfo>p{
  font-size: 12px;
}
</style>