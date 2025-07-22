<template>
  <div class="calculadora">

    <div class="pantalla" :style="{ backgroundColor: pantalla }">
      <div class="display">
        <input class="operacion-display espacio" type="text" name="" id="" v-model="num1">
        <input class="operacion-display" style="width: 10%;" type="text" name="" id="" v-model="operacion">
        <input class="operacion-display espacio" type="text" name="" id="" v-model="num2">
      </div>
      <input class="resultado-display" type="text" name="" id="" v-model="resultado">
    </div>

    <div class="teclado">
      <button class="boton" :disabled="!encendida" @click="limpiar()">🔙</button>
      <button class="boton" @click="onOff()">ON/OFF</button>
      <button class="boton" :disabled="!encendida" @click="borrarNumero()">AC</button>

      <!-- <div class="numeros"> -->
      <button class="boton" @click="darNumero(i)" :disabled="!encendida" v-for="(item, i) in 10" :key="i">{{ i }}
      </button>
      <button class="boton" :disabled="!encendida" @click="darNumero('.')">.</button>
      <!-- </div> -->
      <div class="operaciones">
        <button class="boton" :disabled="!encendida" @click="operacion = '+'">➕</button>
        <button class="boton" :disabled="!encendida" @click="operacion = '-'">➖</button>
        <button class="boton" :disabled="!encendida" @click="operacion = '/'">➗</button>
        <button class="boton" :disabled="!encendida" @click="operacion = '*'">✖️</button>
      </div>
      <button class="boton" :disabled="!encendida" @click="operacion = '%'">%</button>
      <button class="boton grande" :disabled="!encendida" @click="total()"> = </button>
    </div>

  </div>
</template>

<script setup>
import { ref } from "vue"
let num1 = ref('');
let num2 = ref('');
let resultado = ref('');
let operacion = ref(null);
let pantalla = ref('#22223AFF')
let encendida = ref(true)

function darNumero(i) {
  if (!operacion.value) {
    if (i == '.' && num1.value.includes('.')) return;
    num1.value += i;
  } else {
    if (i == '.' && num2.value.includes('.')) return;
    num2.value += i;
  }
  console.log(i);
}

function total() {
  if (operacion.value == '+') {
    resultado.value = "=" + parseFloat(num1.value) + parseFloat(num2.value);
    console.log(resultado.value);
  }
  else if (operacion.value == '-') {
    resultado.value = "=" + parseFloat(num1.value) - parseFloat(num2.value);
    console.log(resultado.value);
  }
  else if (operacion.value == '/') {
    resultado.value = "=" + parseFloat(num1.value) / parseFloat(num2.value);
    console.log(resultado.value);
  }
  else if (operacion.value == '*') {
    resultado.value = "=" + parseFloat(num1.value) * parseFloat(num2.value);
    console.log(resultado.value);
  }
  else if (operacion.value == '%') {
    resultado.value = "=" + parseFloat((num1.value / 100));
  }
  else {
    resultado.value == 'operación inválida❕';
  }
}

function limpiar() {
  num1.value = '';
  num2.value = '';
  resultado.value = '';
  operacion.value = '';
}

function borrarNumero() {
  if (!operacion.value) {
    num1.value = num1.value.slice(0, -1);
  } else {
    num2.value = num2.value.slice(0, -1);
  }
}
function onOff() {
  if (pantalla.value === '#b5d19c') {
    pantalla.value = '#22223AFF';
    encendida.value = false;
    limpiar();
  } else {
    pantalla.value = '#b5d19c';
    encendida.value = true;
    limpiar();
  }
}


</script>

<style scoped>
.calculadora {
  background: linear-gradient(145deg, #6366f1, #4f46e5);
  border-radius: 1rem;
  padding: 1.5rem;
  max-width: 800px;
  width: 55%;
  margin: 2rem auto;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  border: 3px solid #5b21b6;
}

.pantalla {
  background: #8BC34A;
  border-radius: 0.5rem;
  padding: 1rem;
  margin-bottom: 1rem;
  min-height: 80px;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.2);
  border: 2px solid #7B1FA2;
}

/* .display {
  text-align: right;
  width: 100%;
} */

.display {
  display: flex;
}

.operacion-display {
  font-size: 1.8rem;
  color: #2e7d32;
  margin-bottom: 0.2rem;
  min-height: 1.2rem;
  background-color: transparent;
  border: 1px solid transparent;
  text-align: center;
}

.espacio {
  width: 50%;
}

.resultado-display {
  display: flex;
  justify-content: right;
  font-size: 1.8rem;
  font-weight: bold;
  color: #1b5e20;
  font-family: 'Courier New', monospace;
  width: 100%;
  background-color: transparent;
  border: 1px solid transparent;
  text-align: right;
}

.teclado {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}

/* .numeros {
  display: grid;
  grid-template-columns: repeat(3, 20%);
} */

.boton {
  background: linear-gradient(145deg, #9c88c4, #7b68a0);
  color: white;
  border: none;
  padding: 1rem;
  border-radius: 0.5rem;
  font-size: 1.1rem;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  border: 1px solid #5e4c7a;
}

.boton:hover {
  background: linear-gradient(145deg, #b39ddb, #9575cd);
  transform: translateY(-2px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);
}

.boton:active {
  transform: translateY(0);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.boton.especial {
  background: linear-gradient(145deg, #78909c, #607d8b);
  font-size: 0.9rem;
}

.boton.especial:hover {
  background: linear-gradient(145deg, #90a4ae, #78909c);
}

.boton.operador {
  background: linear-gradient(145deg, #8d6e63, #6d4c41);
}

.boton.operador:hover {
  background: linear-gradient(145deg, #a1887f, #8d6e63);
}

.boton.onoff {
  background: linear-gradient(145deg, #ff7043, #e64a19);
  font-size: 0.8rem;
}

.boton.onoff:hover {
  background: linear-gradient(145deg, #ff8a65, #ff7043);
}

.boton.igual {
  background: linear-gradient(145deg, #9c88c4, #7b68a0);
  grid-row: span 1;
}

.boton.igual:hover {
  background: linear-gradient(145deg, #b39ddb, #9575cd);
}

.boton.grande {
  grid-row: span 2;
}

/* Responsive */
@media (max-width: 480px) {
  .calculadora {
    max-width: 280px;
    padding: 1rem;
  }

  .boton {
    padding: 0.8rem;
    font-size: 1rem;
  }

  .resultado-display {
    font-size: 1.5rem;
  }
}
</style>
