<template>
  <div v-if="!validar" class="pantalla">
    <div class="puntaje">
      <div class="contenedor-puntaje">
        Puntaje: <span>{{puntaje}}</span>
      </div>
      <div class="contenedor-intentos">
        Intentos: <span>{{intentos}}</span>
      </div>
    </div>
    <div class="cartas">
      <poke-ventana :nombre="nombres[0]" :imagen="imagenes[0]" />
      <poke-ventana  :nombre="nombres[1]" :imagen="imagenes[1]" />
      <poke-ventana  :nombre="nombres[2]" :imagen="imagenes[2]" />
    </div>
    <button @click="iniciar()">JUGAR</button>
  </div>
  <div v-if="validar" class="mensajes">
    <div v-if="!win" class="lose">
      <h2>Has intentado 5 veces</h2>
      <h2>El juego ha terminado, intentalo nuevamente</h2>
    </div>
    <div v-if="win" class="win">
      <h2>
        Puntaje: <span>{{puntaje}}</span>
      </h2>
      <h2>Felicitaciones has ganado</h2>
    </div>
    <button @click="reiniciar">Nuevo Juego</button>
  </div>
</template>

<script>
import PokeVentana from './PokeVentana.vue';
export default {
  components: { PokeVentana },
    data() {
        return {
        validar: false,
        win: false,
        puntaje: 0,
        intentos: 0,
        nombres: ["xxxxxxxx", "xxxxxxxx", "xxxxxxxx"],
        imagenes: [
            "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg",
            "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg",
            "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg",
        ],
    };
  },
  methods:{
    async consumirApi(){
            const datos_json = await fetch('https://yesno.wtf/api').then(ret=>ret.json())
            console.log(datos_json);
            return datos_json;
        },
    iniciar(){
        console.log(this.nombres);
        console.log(this.imagenes);
        const res1 = this.consumirApi()
        const res2 = this.consumirApi()
        const res3 = this.consumirApi()
        this.nombres= [(this.consumirApi()).answer,(this.consumirApi()).answer,(this.consumirApi()).answer]
        this.imagenes= [this.consumirApi().image,this.consumirApi().image,res3.image]
        console.log(this.nombres);
        console.log(this.imagenes);
      this.jugar(res1.answer,res2.answer,res3.answer);
      this.ganarVerificacion();
    },
    jugar(id1, id2, id3) {
      this.puntaje +=
        id1 == id2 && id2 == id3
          ? 5
          : id1 == id2 || id2 == id3 || id1 == id3
          ? 2
          : 0;
      this.intentos++;
    },
    ganarVerificacion() {
      if (this.intentos < 5) {
        if (this.puntaje >= 10) {
          this.validar = true;
          this.win = true;
        }
      } else {
        this.validar = true;
        this.win = false;
      }
    }
 }

}
</script>

<style>
.pantalla {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.cartas {
width: 750px;
  height: 350px;
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
}
.puntaje {
  display: flex;
  gap: 20px;
}

button {
  width: 150px;
  height: 30px;
}

.mensaje-perder {
  color: red;
}

.mensaje-ganar {
  color: blue;
}
</style>