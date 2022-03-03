<template>
  <div>
    <h1>Vista de un árbol</h1>

    <ul>
      <TreeItem
        class="item"
        :item="treeData"
        @make-folder="makeFolder"
        @add-item="addItem"
      />
    </ul>
  </div>
</template>

<script>
import TreeItem from "./treeItem.vue";
import data from "./data";
export default {
  name: "TreeView",
  components: {
    TreeItem,
  },
  data() {
    return {
      treeData: data,
    };
  },
  methods: {
    makeFolder: function (item) {
      this.$set(item, "children", []);
      this.addItem(item);
    },
    addItem: function (item) {
      item.children.push({
        name: "new stuff",
      });
    },
  },
};
</script>

<style>
body {
  font-family: Menlo, Consolas, monospace;
  color: #444;
}
.item {
  cursor: pointer;
}
.bold {
  font-weight: bold;
}
ul {
  padding-left: 1em;
  line-height: 1.5em;
  list-style-type: dot;
}
</style>
