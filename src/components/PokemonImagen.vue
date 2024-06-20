<template>
    
<div class="container-imagen">
<!--CUANDO ES TRUE ME DA LA IMAGEN-->
   <img v-show="mostrar" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/54.svg" alt="No es posible visualizar la IMAGEN" >
   
   <!--CUANDO ES FALSE ME DA LA IMAGEN-->
   <img v-show="!mostrar" class="oculta-pokemon" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/54.svg" alt="No es posible visualizar la IMAGEN" >
</div>
</template>

<script>
export default {
    data(){
        return{
            mostrar:false,
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