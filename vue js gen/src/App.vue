<script setup>
import { ref } from 'vue';

let hombres = ref([]);
let mujeres = ref([]);

let nombre = ref('');
let edad = ref(0);
let genero = ref('masculino');

const agregarPersona = () => {
  if (nombre.value && edad.value && genero.value) {
    const persona = { nombre: nombre.value, edad: edad.value, genero: genero.value };
    if (genero.value === 'masculino') {
      hombres.value.push(persona);
    } else {
      mujeres.value.push(persona);
    }
    // Limpiar los campos después de agregar la persona
    nombre.value = '';
    edad.value = 0;
    genero.value = 'masculino';
  }
};
</script>

<template>
  <div class="lista">
    <h1>Lista de Géneros</h1>

    <label for="nombre">Nombre:</label>
    <input type="text" v-model="nombre" />

    <label for="edad">Edad:</label>
    <input type="number" v-model="edad" />

    <label for="genero">Género:</label>
    <select v-model="genero">
      <option value="masculino">Masculino</option>
      <option value="femenino">Femenino</option>
    </select>

    <button @click="agregarPersona">Agregar Persona</button>

    <div class="listas">
      <div class="lista-hombres">
        <h2>Listas Hombres</h2>
        <ul>
          <li v-for="(persona, index) in hombres" :key="index">
            {{ persona.nombre }} - {{ persona.edad }} años
          </li>
        </ul>
      </div>

      <div class="lista-mujeres">
        <h2>Listas Mujeres</h2>
        <ul>
          <li v-for="(persona, index) in mujeres" :key="index">
            {{ persona.nombre }} - {{ persona.edad }} años
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.lista {
  margin: auto;
  width: 60%;
  padding: 1em;
  border: 3px solid #3b21ad;
  background-color: #d3f2d8;
}

input {
  width: 100%;
  padding: 8px;
  margin-top: 4px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

label {
  display: block;
  margin-bottom: 10px;
}

.listas {
  display: flex;
  justify-content: space-between;
}

.lista-hombres,
.lista-mujeres {
  width: 45%;
}

ul {
  list-style: none;
  padding: 0;
}
</style>
