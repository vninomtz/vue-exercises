<template>
  <div>
    <h1>Food App</h1>
    <div>
      <label for="search">Buscar</label>
      <input v-model="search" type="text" id="search" />
    </div>
    <div class="food-wrapper">
      <div
        class="food--item"
        v-for="(item, index) in foodFiltered"
        :key="index"
      >
        <strong>{{ item.nombre }}</strong>
        <br />
        Porción recomendada: <em> {{ item.cantidad }}</em>
        <br />
        <code>{{ item.categoria }}</code>
      </div>
    </div>
  </div>
</template>

<script>
import food from "./data";

export default {
  name: "FoodApp",
  data() {
    return {
      food: food,
      search: "",
    };
  },
  computed: {
    foodFiltered() {
      return this.food.filter((item) => {
        if (item.nombre.includes(this.search)) {
          return item;
        }
      });
    },
  },
};
</script>

<style>
.food-wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  max-width: 100%;
  padding: 10px;
}
.food--item {
  margin: 5px;
  padding: 10px;
  background-color: aliceblue;
  border-radius: 10px;
}
</style>
