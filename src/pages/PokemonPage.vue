<template>
    <div>
        <h1>VISUALIZA EL POKEMON CORRECTO</h1>
        <h1 v-if="!pokemonCorrecto">Por favor espere ...</h1>
        <div v-else>
            <PokemonImagen :idPokemon="pokemonCorrecto.id" :mostrarPokemon="mostrar" />
            <div v-if="!respuestaCorrecta">
                <PokemonOpciones :pokemons="arreglo" @seleccionPokemon="revisarRespuesta($event)" />
                <p class="incorrecto" v-if="respuestaIncorrecta" >INCORRECTO - Inténtalo de nuevo</p>
            </div>
            <div v-if="respuestaCorrecta">
                <p>ACERTASTE - EL NOMBRE DEL POKEMON ES: {{ pokemonCorrecto.nombre }}</p>
            </div>
            
        </div>
    </div>
</template>

<script>
import PokemonImagen from '../components/PokemonImagen.vue'
import PokemonOpciones from '../components/PokemonOpciones.vue'
import obtenerPokemonsFachada from '../clientes/ClientePokemonAPI.js'

export default {
    components: {
        PokemonImagen,
        PokemonOpciones
    },
    data() {
        return {
            arreglo: [],
            pokemonCorrecto: null,
            mostrar: false,
            respuestaCorrecta: false,
            respuestaIncorrecta: false
        }
    },
    async mounted() {
        await this.cargaInicial();
    },
    methods: {
        async cargaInicial() {
            const vectorInicial = await obtenerPokemonsFachada(7);
            this.arreglo = vectorInicial;
            const indice = Math.floor(Math.random() * this.arreglo.length);
            this.pokemonCorrecto = this.arreglo[indice];
        },
        revisarRespuesta(dato) {
            if (dato.ident === this.pokemonCorrecto.id) {
                this.mostrar = true;
                this.respuestaCorrecta = true;
                this.respuestaIncorrecta = false;
            } else {
                this.respuestaIncorrecta = true;
            }
        }
    }
};
</script>

<style>
p {
    font-size: 24px;
    color: aliceblue;
}
.incorrecto{
    color: aquamarine;
}
</style>