<template>
  <h2>{{presentar}}</h2>

  <!-- COMENTARIO -->
  

  <p>{{ numero }} <sup>2</sup>={{ calcular }}</p>

  <div>
    <button id="incremetar" @click="incrementar">+1</button>
    <button id="disminuir" @click="disminuir">-1</button>
  </div>
</template>

<script>
export default {

  //YO LA PUEDO USAR COMO UNA PROPIEDAD REACTIVA 
  //PUEDO AÑADIRLE MAS ATRIBUTOS

  // FORMA BASICA DE PROPOR => props:["titulo","num"],

  //FORMA MAS ESTANDARIZADA:
  props:{
    titulo:String,

    num:{

      type: Number,
      required:false, //SI ES REQUERIDO TRUE Y FALSE
      default:10,   //Si no tiene se manda este por DEFECTO

      validator(value){ //Este metodo tiene un RETURN booleano

        return value>0
      }

    }

  },


  data() {
    return {

      numero: this.num,

    };
  },
  methods: {
    calcularCuadrado() {
      console.log("Ingreso al method"); //me imprime 5 veces en la CONSOLA
      return this.numero * this.numero;
    },
    calcularCuadrado2(num1, num2) {
      console.log("Ingreso al method");
      return this.numero * this.numero;
    },
    incrementar(){
      this.numero++;
    },
    disminuir(){
      this.numero--;
    }
  },
  computed: {
    calcular() {
      console.log("Ingreso al PROPIEDAD computada");
      return this.numero * this.numero;
    },
    presentar(){
      if(this.titulo!==undefined){
        return this.titulo;
      }else{
        return 'Texto que Quiero';
      }
    }
  },
};
</script>

<style>
* {
  background-color: beige;
 
 
}
button{
  background-color: #64B687;
  width: 80px;
  height: 30px;
  border-radius: 5px;
  border: 2px solid rgb(7, 7, 7);
  color: white;
  margin: 10px;
  cursor: pointer;

}

button:hover{
  background-color: rgb(3, 75, 85);
  
}



</style>