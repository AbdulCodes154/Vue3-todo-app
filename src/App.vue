<template>
    <h1>Vue 3 todo app</h1>
    <form @submit.prevent="addNewTodo">
        <label>New Todo</label>
        <input v-model="newTodo" name="newTodo">
        <button>Add new todo</button>
    </form>
    <button @click="markAllDone">
        Mark all done
    </button>
    <ul>
        <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
          <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{todo.content}}</h3>
          <button @click="removeTodo(index)">
            Remove todo
          </button>
        </li>
    </ul>
</template>

<script>
import { ref } from 'vue';


export default {
    setup() {
        const newTodo = ref('');
        const todos = ref([]);


        function addNewTodo() {
            todos.value.push({
                id: Date.now(),
                done: false,
                content: newTodo.value,
            });
            newTodo.value = '';
        }

        function toggleDone(todo) {
            todo.done = !todo.done;
        }

        function removeTodo(index) {
            todos.value.splice(index, 1);
        }

        function markAllDone() {
            todos.value.forEach((todo) => todo.done = true);
        }

        return {
            todos,
            newTodo,
            addNewTodo,
            toggleDone,
            removeTodo,
            markAllDone,
        };
    }
}


</script>

<style>

  body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
  }

input, textarea, button, p, div, section, article, select {
  display: 'block';
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
  }
  
.todo {
  cursor: pointer;
  }
  
  .done {
    text-decoration: line-through;
  }

  .todo {
    cursor: pointer;
  }

</style>