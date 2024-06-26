<template>
    <div>
        <h1>QUIEN ES ESE POKEMON?</h1>
        <div class="puntaje-intentos">
            <p>Puntaje: {{ puntaje }}</p>
            <p>Intentos: {{ intentos }}</p>
        </div>
        
        <h1 v-if="!pokemonCorrecto">Por favor espere ...</h1>
        <div v-else>
            <PokemonImagen :idPokemon="pokemonCorrecto.id" :mostrarPokemon="mostrar" />
            <div v-if="!respuestaCorrecta">
                <PokemonOpciones :pokemons="arreglo" @seleccionPokemon="revisarRespuesta($event)" />
                <p  class="incorrecto" v-if="respuestaIncorrecta">INCORRECTO - Inténtalo de nuevo</p>
            </div>
            <div v-if="respuestaCorrecta">
                <p>Es...: {{ pokemonCorrecto.nombre }}</p>
            </div>
        </div>
        
        <button @click="reiniciarJuego">Reiniciar</button>
    </div>
</template>

<script>
import PokemonImagen from '../components/PokemonImagen.vue';
import PokemonOpciones from '../components/PokemonOpciones.vue';
import obtenerPokemonsFachada from '../clientes/ClientePokemonAPI.js';

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
            respuestaIncorrecta: false,
            puntaje: 0,
            intentos: 0
        };
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
            this.mostrar = false;
            this.respuestaCorrecta = false;
            this.respuestaIncorrecta = false;
            this.intentos = 0;
            this.puntaje = 0;
        },
        revisarRespuesta(dato) {
            this.intentos++;
            if (dato.ident === this.pokemonCorrecto.id) {
                this.mostrar = true;
                
                this.respuestaCorrecta = true;
                this.respuestaIncorrecta = false;
                this.puntaje = this.calcularPuntaje();
            } else {
                this.respuestaIncorrecta = true;
                if (this.intentos >= 7) {
                    alert('¡Se acabaron los intentos!');//FUNCIONA COMO UN SNACKBAR 
                    this.reiniciarJuego();
                }
            }
        },
        calcularPuntaje() {
            switch (this.intentos) {
                case 1: return 10;
                case 2: return 8;
                case 3: return 5;
                case 4: return 3;
                case 5: return 2;
                case 6: return 1;
                case 7: return 0;
                default: return 0;
            }
        },
        reiniciarJuego() {
            this.cargaInicial();
        }
    }
};
</script>

<style>
p {
    font-size: 24px;
    color: aliceblue;
}
.incorrecto {
    color: rgb(176, 245, 222);
}
.puntaje-intentos{
    display: flex;
    justify-content: center;
    align-content: center;
    gap: 50px;

}
</style>
