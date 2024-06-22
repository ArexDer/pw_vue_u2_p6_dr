<template>
    <div class="container-opciones">
        <ul>
            <li v-for="pokemon in pokemons" :key="pokemon.id"
                @click="$emit('seleccionPokemon', { ident: pokemon.id, nomb: pokemon.nombre, test: 'esto es una prueba' ,test2:test3})">
                {{ pokemon.nombre }}
            </li>
        </ul>

    </div>

</template>

<script>
export default {
    props: {
        pokemons: {
            type: Array,
            required: true
        },
    },
    data(){
        return{
            test3:'Segunda Prueba'
        }
    }
}
</script>

<style>
ul {
    list-style-type: none;

}

li {
    border: 2px solid rgb(114, 62, 62);
    border-radius: 5px;
    margin-bottom: 12px;
    width: 200px;
    background-color: aliceblue;
    color: black;
    cursor: pointer;
    padding: 15px;
}

li:hover {
    background-color: black;
    color: white;
}

.container-opciones {

    display: flex;
    justify-content: center;
}
</style>