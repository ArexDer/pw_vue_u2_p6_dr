<template>
    <h1>VISUALIZA EL POKEMON CORRECTO</h1>
  <PokemonImagen :idPokemon="54"  :mostrarPokemon="false"/>
  <PokemonOpciones :pokemons="arreglo"/>

</template>

<script>
import PokemonImagen  from '../components/PokemonImagen.vue'
import PokemonOpciones  from '../components/PokemonOpciones.vue'

//AQUI VA EL NOOMBRE DEL METODO DE EXPORTACION.
import obtenerPokemonsFachada from '../clientes/ClientePokemonAPI.js'

export default {

    components:{
        PokemonImagen,
         PokemonOpciones
    },

    methods:{
        async cargaInicial(){
            const vectorInicial = await obtenerPokemonsFachada(4)
            this.arreglo=vectorInicial
            
        },
    },

    //PROPIEDAD RECTIVA
    data(){
        return{
            arreglo:[],
            

        }
    },

    //REPRESENTA MONTAR EL COMPONENTE DENTRO DE LA PAGINA.
    //CICLO DE VIDA...
    mounted(){
        this.cargaInicial();

    }
    

};
</script>

<style>

</style>