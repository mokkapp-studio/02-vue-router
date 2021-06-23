<template>
    <Titulo texto="Titulo del blog"/>
    <span>Método create( ): se llama sin función de felcha, porque la función de flecha no tiene acceso al this</span>
    <br>
    <button @click="getAPI" disabled>Consumir API</button>
    <div v-for="resultado in arrayBlog" :key="resultado.id">
        <router-link :to="`/blog/${resultado.id}`">
            <p>{{resultado.id}} - {{resultado.title}}</p>
        </router-link>
    </div>
</template>

<script>
import Titulo from '../components/Titulo.vue'
export default {
    components: { 
      Titulo 
    },
    data() {
        return {
            arrayBlog: []
        }
    },
    methods: {
        async getAPI() {
            try {
                const dataAPI = await fetch('https://jsonplaceholder.typicode.com/posts')
                const resultados = await dataAPI.json()
                console.log(resultados)
                this.arrayBlog = resultados;
            } catch (error) {
                console.log(error)
            }
        }
    },
    created(){
        this.getAPI()
    }
}
</script>

<style>

</style>