<script setup>
import { computed, reactive, ref } from "vue";
import taylorImage from "@/assets/images/ts.png"

const todos = reactive([
  { id: crypto.randomUUID(), text: "Watch The Eras Tour Movie", completed: true },
  { id: crypto.randomUUID(), text: "Get new Taylor merch", completed: false },
]);

const inputToDo = ref("");

const pendingCount = computed(() => todos.filter((t) => !t.completed).length);

function addTodo() {
  const text = inputToDo.value.trim();
  if (!text) return;

  todos.push({
    id: crypto.randomUUID(),
    text,
    completed: false,
  });

  inputToDo.value = "";
}

function removeTodo(id) {
  const idx = todos.findIndex((t) => t.id === id);
  if (idx !== -1) todos.splice(idx, 1);
}

function toggleCompletion(id) {
  const todo = todos.find((t) => t.id === id);
  if (todo) todo.completed = !todo.completed;
}

function clearCompleted() {
  for (let i = todos.length - 1; i >= 0; i--) {
    if (todos[i].completed) todos.splice(i, 1);
  }
}

function clearAll() {
  todos.splice(0, todos.length);
}
</script>

<template>
  <section class="task">
    <h1 class="title">🎶Intermediate Level | Tay-Do List</h1>
    <img :src="taylorImage" class="corner-image" alt="Taylor-Swift" />

    <div class="form">
      <input type="text" v-model="inputToDo" placeholder="New Task" @keydown.enter.prevent="addTodo" />
      <button class="addBtn" type="button" @click="addTodo">+</button>
    </div>

    <ul class="taskItems">
      <li v-for="todo in todos" :key="todo.id">
        <button class="toggle" :class="{ 'toggle-completed': todo.completed }" type="button"
          @click="toggleCompletion(todo.id)">
          <span class="bullet">{{ todo.completed ? "●" : "○" }}</span>
          <span class="text">{{ todo.text }}</span>
        </button>

        <button class="delete" type="button" @click="removeTodo(todo.id)">🗑️</button>
      </li>
    </ul>

    <div class="clearBtns">
      <button type="button" class="btn-clear" @click="clearCompleted">
        Clear completed
      </button>

      <button type="button" class="btn-clear-all" @click="clearAll">
        Clear all
      </button>
    </div>


    <p class="pendingTasks">Pending Tasks: <strong>{{ pendingCount }}</strong></p>
  </section>
</template>


<style scoped>
.task {
  background: var(--card-bg);
  border-radius: 25px;
  padding: 30px;
  box-shadow: var(--shadow);
  position: relative;
  padding-bottom: 240px;
}

.title {
  text-align: center;
  margin: 0 0 20px;
  font-size: 22px;
}

.form {
  position: relative;
  margin: 0 0 30px;
}

.form input[type="text"] {
  width: 100%;
  height: 50px;
  font: inherit;
  padding: 15px;
  background: var(--input-bg);
  color: var(--text);
  border: 1px solid transparent;
  border-radius: 10px;
  transition: border 0.3s linear;
}

.form input[type="text"]:focus {
  outline: none;
  border: 1px solid var(--accent);
}

.addBtn {
  background: none;
  border: none;
  color: var(--accent);
  font-size: 22px;
  position: absolute;
  top: 50%;
  right: 18px;
  transform: translateY(-50%);
  cursor: pointer;
}

.clearBtns {
  display: flex;
  justify-content: space-between;
  margin: 0 0 20px;
  gap: 10px;
}

.clearBtns button {
  width: 100%;
  color: #fff;
  border: none;
  border-radius: 10px;
  padding: 10px;
  cursor: pointer;
  transition: background 0.2s ease;
}

.btn-clear {
  background: #4ea9c8;
}

.btn-clear:hover {
  background: #3f8fae;
}

.btn-clear-all {
  background: #ea7ba6;
}

.btn-clear-all:hover {
  background: #d96a95;
}

.taskItems {
  padding: 0 10px;
  list-style: none;
  margin: 0 0 20px;
}

.taskItems li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 0 18px;
}

.toggle {
  background: none;
  border: none;
  cursor: pointer;
  text-align: left;
  display: inline-flex;
  align-items: center;
  gap: 10px;
  color: var(--text);
  padding: 0;
  font: inherit;
  flex: 1;
  min-width: 0;
}

.toggle .text {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.toggle.toggle-completed .text {
  text-decoration: line-through;
  color: var(--muted);
}

.bullet {
  font-size: 14px;
  width: 18px;
  display: inline-flex;
  justify-content: center;
}

.delete {
  background: none;
  border: none;
  cursor: pointer;
  padding: 2px 6px;
  font-size: 16px;
}

.pendingTasks {
  padding: 0 6px;
  color: var(--text);
}

.corner-image {
  position: absolute;
  bottom: 0;
  right: 0;
  margin: 0 16px;
  width: 280px;
}

@media (max-width: 768px) {
  .corner-image {
    width: 200px;
  }
}
</style>