<template>
  <Titulo texto="texto con parámetros"/>
  <h2>Parámetro: {{$route.params.id}}</h2> 
  <h3>{{resultado.title}}</h3>
  <p>{{resultado.id}}:{{' '}}{{resultado.body}}</p>
</template>

<script>
import Titulo from '../components/Titulo.vue'

export default {
    components: {
        Titulo
    },
    data() {
        return {
            resultado: {}
        }
    },
    methods: {
        async detalleArticulo(){
            try {
                const data = await fetch(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
                const objeto = await data.json()
                this.resultado = objeto
                console.log(objeto)
            } catch (error) {
                console.log(error)
            }
        }
    },
    created(){
        this.detalleArticulo()
    }
}
</script>

<style>

</style>