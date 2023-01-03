<template>
  <li class="todo-item" draggable="true">
    {{ item.name }}
    <button @click="deteteItem(item.id)">X</button>
  </li>
</template>

<style>
.todo-item {
  border-radius: 5px;
  background-color: #d4f1f4;
  width: 220px;
  padding: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: medium;
  margin: 10px 0;
  cursor: move;
}
.todo-item button {
  background-color: #f56;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  font-size: medium;
  color: #d4f1f4;
  font-weight: bold;
  cursor: pointer;
}
</style>

<script>
export default {
  name: "TodoItem",
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  methods: {
    deteteItem(id) {
      this.$emit("delete-item", id);
    },
  },
};
</script>
