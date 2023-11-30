<script setup lang="ts">
import {ref} from 'vue'
  type ToDo = {
    id: number,
    title: string,
    completed: boolean,
  } 

  const list = ref<ToDo[]> ([
    {
      id: 1,
      title: "ciao",
      completed: false,
    },
    {
      id: 2,
      title: "hello",
      completed: false,
    },
    {
      id: 3,
      title: "hola",
      completed: true,
    }
])
const newItem = ref('')
function addOne() {
list.value.push({
  id: list.value.length + 1,
  title: newItem.value,
  completed: false,
})
}
</script>

<template>
  <main class="container mt-4 bg-blue-500">
    <form @submit.prevent="addOne">
      <input type="text" v-model="newItem" placeholder="add title">
      <button type="submit" @click="addOne">
        add
      </button>
    </form>
    <li v-for="item in list" :key="item.id">
      {{ item.title }}
    </li>
  </main>
</template>
