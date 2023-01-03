<template>
  <div class="home">
    <h1>Todo List</h1>
    <div class="input-box">
      <input type="text" v-model="newItem" @keyup.enter="createItem" />
      <button type="submit" @click="createItem">Create</button>
    </div>

    <div class="state-lists">
      <div
        class="drop-zone todo-list"
        @drop="onDrop($event, 'todo')"
        @dragover.prevent
        @dragenter.prevent
      >
        <h3>To Do</h3>
        <ul>
          <TodoListItem
            v-for="item in toDoItems"
            :key="item.id"
            :item="item"
            @delete-item="deteteItem"
            @dragstart="startDrag($event, item)"
          />
        </ul>
      </div>
      <div
        class="drop-zone doing-list"
        @drop="onDrop($event, 'doing')"
        @dragover.prevent
        @dragenter.prevent
      >
        <h3>Doing</h3>
        <ul>
          <TodoListItem
            v-for="item in doingItems"
            :key="item.id"
            :item="item"
            @delete-item="deteteItem"
            @dragstart="startDrag($event, item)"
          />
        </ul>
      </div>
      <div
        class="drop-zone done-list"
        @drop="onDrop($event, 'done')"
        @dragover.prevent
        @dragenter.prevent
      >
        <h3>Done</h3>
        <ul>
          <TodoListItem
            v-for="item in doneItems"
            :key="item.id"
            :item="item"
            @delete-item="deteteItem"
            @dragstart="startDrag($event, item)"
          />
        </ul>
      </div>
    </div>
  </div>
</template>

<style>
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.input-box input {
  width: 300px;
  height: 30px;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 5px;
  margin: 10px;
}
.input-box button {
  background-color: #05445e;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  font-size: medium;
  color: #d4f1f4;
  font-weight: bold;
}
.state-lists {
  display: flex;
  justify-content: space-between;
  width: 900px;
  margin-top: 40px;
}
.drop-zone {
  width: 300px;
  min-height: 300px;
  border: 1px solid #ccc;
  border-radius: 20px;
  background-color: #d1dfd1;
  padding: 10px;
  margin: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.todo-list {
  background-color: #e0b0b0;
}
.doing-list {
  background-color: #b0b0e0;
}
.done-list {
  background-color: #b0e0b0;
}
ul {
  padding: 0;
  margin: 0;
}
</style>

<script>
import TodoListItem from "@/components/TodoListItem.vue";

export default {
  name: "HomeView",
  components: {
    TodoListItem,
  },
  data() {
    return {
      newItem: "",
      currentIndex: 3,
      states: ["todo", "doing", "done"],
      items: [
        {
          id: 1,
          name: "Item 1",
          state: "todo",
        },
        {
          id: 2,
          name: "Item 2",
          state: "doing",
        },
        {
          id: 3,
          name: "Item 3",
          state: "done",
        },
      ],
    };
  },
  methods: {
    createItem() {
      if (this.newItem === "") {
        return;
      }
      this.items.push({
        id: this.currentIndex + 1,
        name: this.newItem,
        state: "todo",
      });
      this.newItem = "";
      this.currentIndex++;
      console.log("createItem", this.items);
    },

    deteteItem(id) {
      this.items = this.items.filter((item) => item.id !== id);
      console.log("deteteItem");
    },

    startDrag(evt, item) {
      evt.dataTransfer.dropEffect = "move";
      evt.dataTransfer.effectAllowed = "move";
      evt.dataTransfer.setData("itemID", item.id);
    },

    onDrop(evt, state) {
      const itemID = parseInt(evt.dataTransfer.getData("itemID"));
      const item = this.items.find((item) => item.id === itemID);
      item.state = state;
    },
  },

  computed: {
    toDoItems() {
      return this.items.filter((item) => item.state === "todo");
    },
    doingItems() {
      return this.items.filter((item) => item.state === "doing");
    },
    doneItems() {
      return this.items.filter((item) => item.state === "done");
    },
  },
};
</script>
