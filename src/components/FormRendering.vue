<script>
export default {
  name: 'FormRendering',
  data() {
    return {
      colorFondo: '',
      colorTexto: '',
      texto: true,
      borde: '',
      contenido: '',
      tipografia: ['cursive', 'monospace', 'serif', 'sans-serif'],
      tipografiaSelected: '',
      opaco: '',
      sizeLetra: [
        { value: 'small', label: 'Pequeño' },
        { value: 'large', label: 'Mediano' },
        { value: 'xxx-large', label: 'Grande' }
      ],
      sizeLetraSelected: ''
    }
  }
}
</script>

<template>
  <div class="box-container">
    <form class="form-container">
      <label for="colorFondo">Color de fondo:</label>
      <input type="color" id="colorFondo" v-model="colorFondo" />

      <label for="colorTexto">Color de texto:</label>
      <input type="color" id="colorTexto" v-model="colorTexto" />

      <div class="flex">
        <label for="texto">Mostrar texto</label>
        <input type="checkbox" id="texto" v-model="texto" />
      </div>

      <label for="borde">Borde:</label>
      <input type="range" min="0" max="50" id="borde" v-model="borde" />

      <label for="contenido">Escribe un mensaje</label>
      <textarea id="contenido" v-model="contenido"></textarea>

      <label for="tipografia">Tipografía:</label>
      <select id="tipografia" v-model="tipografiaSelected">
        <option v-for="tipografia in tipografia" :key="tipografia" :value="tipografia">
          {{ tipografia }}
        </option>
      </select>

      <div class="flex">
        <label for="opaco">Opaco</label>
        <input type="checkbox" id="opaco" v-model="opaco" />
      </div>

      <div class="flex">
        <label for="tamañoDeLetra">Tamaño de letra:</label>
        <div class="check-item flex" v-for="tamano in sizeLetra" :key="tamano.value">
          <label :for="tamano.value">{{ tamano.label }}</label>
          <input
            type="radio"
            :id="tamano.value"
            :value="tamano.value"
            v-model="sizeLetraSelected"
          />
        </div>
      </div>
    </form>

    <div
      id="resultado"
      :style="{
        backgroundColor: colorFondo,
        color: colorTexto,
        borderRadius: borde + '%',
        fontFamily: tipografiaSelected,
        fontSize: sizeLetraSelected
      }"
      :class="{
        opaco: opaco
      }"
    >
      <p v-show="texto">{{ contenido }}</p>
    </div>
  </div>
</template>

<style scoped>
.box-container {
  display: flex;
  gap: 2rem;
  align-items: center;
}

.form-container {
  display: flex;
  flex-direction: column;
  align-items: start;
  gap: 10px;
  padding-inline: 2.5rem;
  padding-block: 2rem;
  background-color: #191d8a;
  color: white;
}

#resultado {
  width: 450px;
  height: 450px;
  display: grid;
  place-content: center;
}

.flex {
  display: flex;
  gap: 10px;
}

input[type='range'] {
  width: 100%;
}

select {
  width: 100%;
  padding: 5px;
}
textarea {
  width: 100%;
  height: 100px;
}
.opaco {
  opacity: 0.5;
}
</style>
