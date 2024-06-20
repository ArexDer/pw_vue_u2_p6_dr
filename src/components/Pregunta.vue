<template>
<img v-if="img"
v-bind:src="img"
    alt="No se pudo"
/>

<div class="oscuro"></div>
<div class="pregunta-container">
    <input v-model="pregunta" type="text" placeholder="Realizame una pregunta" />
    <p>Recuerda Terminar la pregunta con el Signo de INTERROGACION (?)</p>


    <div v-show="mensaje" class="respuesta">

<h2>{{ pregunta }}</h2>

<h1>{{ respuesta ==='yes' ?'SI!':'NO!'}}</h1>
    </div>
</div>
</template>

<script>
export default {
    data(){
        return{
            pregunta:null,
            respuesta:null,
            img:null,
            mensaje:false
        }
    },

    watch:{
        pregunta(value, oldValue){
            this.mensaje=false
            console.log({value ,oldValue});
            if(!value.includes("?")){
                return;//Salgase del observador
            } 
            //CONSUMIR EL -----API -----
            this.obtenerRespuesta();
            this.mensaje=true
        },
    },
    methods:{
        async obtenerRespuesta(){
            this.respuesta="pensando..."
            
            //await ESPERA QUE AL API RESPONDA fetch('Url del API').then(respuesta => respuesta.json())
            const data=await fetch('https://yesno.wtf/api').then(resp =>resp.json())
            console.log(data);
           //Simepre cuando mi metodo tiene un AWAIT debo declararlo al metodo como ASINCRONO
            const{answer,forced,image}=data;
            console.log(answer);
            this.respuesta=answer;
            this.img=image;
            return data;
        }
    },
};
</script>


<style scoped>
img,
.oscuro {
max-height: 100%;
height: 100vh;
width: 100vw;
max-width: 100%;
position: fixed;
/*FIXED: Se refiere a  quitar la distribucion que es uno despues
    de otro
    */
/*Para que inicie desde arriba y desde la izquierda*/
top: 0px;
left: 0px;

}

.oscuro {
background-color: rgba(131, 68, 68, 0.3);
/* 0.0 full traspararente y 1.0 FULL OPACO*/
}

.pregunta-container {
position: relative;
}

input{
    width: 260px;
    padding: 15px 10px;
    border: none;
    border-radius: 5px;
    margin-top: 100px;
    text-align: center;
    content: center;
}

input:focus{
    outline:none;
    
    /* */
}
p,h1,h2{
    color:rgb(255, 255, 255);
    
}

p{
    font-size: 28px;
    margin-top: 0px;
}
.respuesta{
    margin-top: 150px;
}


</style>
