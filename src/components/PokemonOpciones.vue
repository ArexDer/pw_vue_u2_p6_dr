<template>
    <div class="container-opciones">
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>

           <!--<li v-for="" item from lista></li> --> 
        </ul>

    </div>

</template>

<script>
export default {

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