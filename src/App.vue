<template>
  <!-- <Listitem
    v-for="(item, index) in dataBase"
    :name="item.name"
    :department="item.Department"
    :salary="item.salary"
    :position="index"
    :key="item"
  /> -->
  <main id="app">
    <section class="greeting">
      <h2 class="title">
        what's up, <input type="text" placeholder="Name here" v-model="name" />
      </h2>
    </section>
    <section class="create-todo">
      <h3>CREATE A TODO</h3>
      <form @submit.prevent="addTodo">
        <h4>what's on your todo list?</h4>
        <input
          type="text"
          placeholder="eg make a video"
          v-model="input_content"
        />

        <h4>Pick a category</h4>
        <div class="options">
          <label>
            <input
              type="radio"
              name="category"
              value="business"
              v-model="input_category"
            />
            <span class="bubble business"></span>
            <div>personal</div>
          </label>
          <label>
            <input
              type="radio"
              name="category"
              value="personal"
              v-model="input_category"
            />
            <span class="bubble personal"></span>
            <div>category</div>
          </label>
        </div>
        <input type="submit" value="" />
      </form>
    </section>
    <section class="todo-list">
      <h3>TODO LISt</h3>
      <div class="list">
        <div
          v-for="todo in todos_asc"
          :class="`todo-item ${todo.done && 'done'}`"
        >
          <label>
            <input type="checkbox" v-model="todo.done" />
            <span :class="`bubble ${todo.category}`"></span>
          </label>

          <div class="todo-content">
            <input type="text" v-model="todo.content" />
          </div>

          
            <div class="actions">
              <button class="delete" @click="removeTodo(todo)">Delete</button>
            </div>
         
        </div>
      </div>
    </section>
  </main>
</template>

<script setup>
import { computed, onMounted, ref, watch } from "vue";
import Listitem from "./components/Database.vue";
const todos = ref([]);
const name = ref("");
const input_content = ref("");
const input_category = ref(null);

const todos_asc = computed(() =>
  todos.value.sort((a, b) => {
    return b.createdAt - a.createdAt;
  })
);
const addTodo = () => {
  if (input_content.value === "" || input_category.value === null) {
    return;
  }
  todos.value.push({
    content: input_content.value,
    category: input_category.value,
    createdAt: new Date().getTime(),
    done: false,
  });
  input_content.value = "";
  input_category.value = null;
};
const removeTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo);
};
watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  { deep: true }
);
watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});
onMounted(() => {
  localStorage.getItem("name") || "";
  todos.value = JSON.parse(localStorage.getItem("todos")) || [];
});

</script>

<style scoped>
.fade-enter-from {
  opacity: 0;
}
.fade-enter-to {
  opacity: 1;
}
.fade-enter-active {
  transition: all 5s ease;
}
</style>
