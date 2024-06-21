<template>
    
<div class="container-imagen">
<!--CUANDO ES TRUE ME DA LA IMAGEN-->
   <img v-show="mostrarPokemon" :src="imagenFuente" >
   
   <!--CUANDO ES FALSE ME DA LA IMAGEN-->
   <img v-show="!mostrarPokemon" class="oculta-pokemon" :src="imagenFuente" alt="No es posible visualizar la IMAGEN" >
</div>
</template>

<script>
export default {

    data(){
        return{
            mostrar:false,
            

        }
    },
    props:{
        idPokemon:{
            type: Number,
            required: true
        },

        mostrarPokemon:{
            type: Boolean,
            required: true
        }
    },

    computed:{
        imagenFuente(){
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.idPokemon}.svg`;

        }

    }
}
</script>


<style scoped>
.oculta-pokemon{
    filter: brightness(0);
}

img{

    height: 200px;
    width:  250px;
    position: absolute;
    right: 38%;
}

.container-imagen{
    height: 200px;
}


</style>