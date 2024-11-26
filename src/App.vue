<template>

  <Layout>
    <template #header>
      <slot name="header"></slot>
    </template>
    <template #aside>
      <slot name="aside"></slot>
    </template>
    <template #main>
      <slot name="main"></slot>
    </template>
    <template #footer>
      <slot name="footer"></slot>
    </template>
  </Layout>

  <form @submit.prevent="addTodo">
    <fieldset role="group">
      <input type="text" placeholder="Ajouter une tâche" v-model="newTodo" />
      <button :disabled="newTodo.length == 0">Ajouter</button>
    </fieldset>
  </form>

  <div v-if="todos.length === 0">Pas de tâche à faire</div>
  <div v-else>
    <ul>
      <li
        v-for="todo in sortedTodos"
        :key="todo.date"
        :class="{ completed: todo.completed }"
      >
      <Checkbox :label="todo.title"  v-model="todo.completed" /> 
      </li>
    </ul>
    <label>
      <input type="checkbox" v-model="hideCompleted" />
      masquer les tâches terminées
    </label>
    <p v-if="remainingTodos > 0">{{ remainingTodos }} tâches restantes</p>
   
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import Checkbox from './Checkbox.vue';
import Button from './Button.vue';
import Layout from './Layout.vue';

const todos = ref([
  {
    title: 'Tâche 1',
    completed: false,
    date: Date.now() + Math.random()
  }
]);

const hideCompleted = ref(false);

const newTodo = ref('');

const addTodo = () => {
  if (!newTodo.value.trim()) return;
  todos.value.push({
    title: newTodo.value.trim(),
    completed: false,
    date: Date.now() + Math.random()
  });
  newTodo.value = '';
};

const sortedTodos = computed(() => {
  const sorted = [...todos.value].sort((a, b) =>
    a.completed > b.completed ? 1 : -1
  );
  if (hideCompleted.value) {
    return sorted.filter(t => !t.completed);
  }
  return sorted;
});

const remainingTodos = computed(() => {
  return todos.value.filter(t => !t.completed).length;
});
</script>

<style>
.completed {
  opacity: 0.4;
  text-decoration: line-through;
}
</style>
