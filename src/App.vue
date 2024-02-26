<script lang="ts">

type Todo = {
  id: number;
  title: string;
  checked: boolean;
}
export default {
  data() {
    return {
      todo: {
        title: '',
        checked: false
      },
      todos: [
        { id: 1, title: 'eat', checked: true },
        { id: 2, title: 'work', checked: false },
        { id: 3, title: 'sleep', checked: false },
        { id: 4, title: 'repeat', checked: false },
      ]
    }
  },
  methods: {
    addTodo(todo: Omit<Todo, 'id' | 'checked'>) {
      if (!todo.title) {
        return
      }
      this.todos.push({ id: this.todos.length + 1, checked: false, ...todo })
      this.todo.title = ''
    },
    deleteTodo(id: number) {
      this.todos = this.todos.filter((todo) => todo.id != id)
    }
  }
}
</script>

<template>
  <div class="app">
    <h1>ToDo App 💩</h1>
    <h2 class="api">Options API</h2>
    <div class="wrapper">
      <form class="add-form">
        <input type="text" class="form-input" v-model="todo.title" />
      </form>
      <button @click="addTodo(todo)" class="add-btn">Add todo</button>
    </div>
    <h2 v-if="!todos.length">No tasks to do 😎</h2>
    <ul v-else>
      <li v-for="todo in todos" :key="todo.id">
        <span :class="{checked:todo.checked}">{{ todo.title }}</span>
        <input type="checkbox" id="checkbox" v-model="todo.checked" />
        <button class="delete-btn" @click="deleteTodo(todo.id)">x</button>
      </li>
    </ul>

  </div>
</template>

<style scoped>
ul {
  list-style: none;
  font-size: 24px;
}

li {
  display: flex;
  gap: 10px;
  align-items: center;
}

.api {
  color: lightgrey;
}

.wrapper {
  display: flex;
  gap: 20px;
  align-items: center;
  margin: 20px 0px;
  padding-top: 10px;
  border-top: gray solid 1px;
  width: 40%;
}

.form-input {
  width: 300px;
  border: grey solid 1px;
  border-radius: 10px;
  padding: 10px;
}

.add-btn {
  cursor: pointer;
  padding: 10px;
  background-color: blue;
  border-radius: 10px;
  border: none;
  color: white;
  font-weight: bold;
}

.delete-btn {
  border: none;
  background-color: white;
  color: red;
  cursor: pointer;
}

.checked {
  color: gray;
  text-decoration: line-through;
}</style>
