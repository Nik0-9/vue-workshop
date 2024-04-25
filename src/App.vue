<template>
  <div class="container ">
    <h1>
      Workshop
    </h1>
    <div class="d-flex justify-content-between align-content-center">
      <h2>Colors</h2>
      <div>
        <select name="palette" id="palette" v-model="selectedPalette">
          <option value="">All</option>
          <option value="fire">Fire</option>
          <option value="summer">Summer</option>
        </select>
        <button @click="filterPalette">Filter</button>
      </div>
    </div>
    <div class="d-flex justify-content-center mt-3 ">
      <div v-for="(color, index) in this.filteredColors" :key="index" class="circle"
        :style="{ backgroundColor: color.hex }" @click="setActive(index)">
      </div>
    </div>
    <div class="box" :style="{ backgroundColor: filteredColors[active].hex }">
        <h5>Nome: {{ filteredColors[active].label }}</h5>
        Hex: {{ filteredColors[active].hex }}
    </div>
  </div>
</template>

<script>
import { store } from './store.js';
export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      store,
      active: 0,
      selectedPalette: '',
      filteredColors: []
    }
  },
  methods: {
    setActive(index) {
      this.active = index;
    },
    filterPalette() {
      this.filteredColors = store.colors.filter((color) => {
        if (color.palette_name === this.selectedPalette || this.selectedPalette === "") {
          return true;
        } else {
          return false;
        }
      });
    },
    getFilterColor() {
      console.log(store.colors);
      return this.filteredColors = store.colors;
    }
  },
  created() {
    this.getFilterColor()
  }
}
</script>

<style lang="scss" scoped>
h1 {
  text-align: center;
  padding: 10px 0px;
}

.circle {
  background-color: red;
  height: 50px;
  aspect-ratio: 1 / 1;
  border-radius: 50%;
  border: 1px solid black;
  margin: 10px;
}

.box {
  height: 200px;
  width: 500px;
  border: 1px solid black;
  margin: 50px auto;
  color: white;
  font-size:x-large;

}

.card {
  width: 500px;
  height: 200px;
  border: 1px solid black;
}
</style>