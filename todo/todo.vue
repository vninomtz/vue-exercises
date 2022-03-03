<template>
  <div>
    <h1>TodoApp</h1>
    <div>
      <label for="inputtask">Agregar tarea: </label>
      <input
        v-model="task"
        type="text"
        key="inputtask"
        @keyup.enter="createTask"
      />
      <button @click="createTask">Agregar</button>
    </div>
    <div>
      <h4>Filtros</h4>
      <div>
        <input
          v-model="filter"
          type="radio"
          id="all"
          name="filters"
          value="all"
          checked
        />
        <label for="all">Todos</label>
      </div>

      <div>
        <input
          v-model="filter"
          type="radio"
          id="completed"
          name="filters"
          value="completed"
        />
        <label for="completed">Completados</label>
      </div>

      <div>
        <input
          v-model="filter"
          type="radio"
          id="archived"
          name="filters"
          value="archived"
        />
        <label for="archived">Archivados</label>
      </div>
    </div>
    <div>
      <div
        class="todo--item"
        v-for="(item, index) in itemsFiltered"
        :key="index"
      >
        <span>{{ index }} - {{ item.title }}</span>
        <input
          v-model="item.completed"
          type="checkbox"
          name="Completada"
          id=""
        />
        <button @click="archiveTask(item)">
          {{ item.archived ? "Desarchivar" : "Archivar" }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import items from "./data";

export default {
  name: "TodoVue",
  data() {
    return {
      items: items,
      task: "",
      filter: "all",
    };
  },
  computed: {
    itemsFiltered() {
      return this.items.filter((item) => {
        if (this.filter === "all") {
          return item;
        }
        if (this.filter === "completed" && item.completed) {
          return item;
        }
        if (this.filter === "archived" && item.archived) {
          return item;
        }
      });
    },
  },
  methods: {
    createTask() {
      var created = new Date(Date.now());
      var newTask = {
        title: this.task,
        completed: false,
        created: created.toLocaleString(),
      };
      this.items.push(newTask);
      this.task = "";
    },
    archiveTask(item) {
      var index = this.items.indexOf(item);
      this.items[index].archived = !item.archived;
    },
    removeTask(item) {
      var index = this.items.indexOf(item);
      this.items.splice(index, 1);
    },
  },
};
</script>

<style>
.todo--item {
  margin: 10px;
  display: flex;
  align-content: center;
  background-color: rgba(0, 0, 0, 0.075);
}
</style>
