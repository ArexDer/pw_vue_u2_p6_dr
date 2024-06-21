<template>
    <div class="container-opciones">
        <ul>
           
          <li v-for="pokemon in pokemons" :key="pokemon.id">{{ pokemon.name }}</li>
        </ul>

    </div>

</template>

<script>
export default {
    props:{
        pokemons:{
            type: Array,
            required: true
        },
    },
}
</script>

<style>

ul{
    list-style-type: none;
    
}
li{
    border: 2px solid rgb(114, 62, 62);
    border-radius: 5px;
    margin-bottom: 12px;
    width: 200px;
    background-color: aliceblue;
    color: black;
    cursor: pointer;  
    padding: 15px;
}

li:hover{
    background-color: black;
    color: white;
}

.container-opciones{

    display: flex;
    justify-content: center;
}

</style>