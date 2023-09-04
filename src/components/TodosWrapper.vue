<template>
  <div>
    <div>
      <form @submit.prevent="addTodo">
        <input type="text" v-model="form.title" />
        <textarea rows="5" v-model="form.desc"></textarea>
        <button type="submit">Save</button>
      </form>
    </div>

    <TodoTable :todos="tableData" @delete="deleteTodo">
      <template #filter>
        <input type="text" v-model="search" placeholder="Search Todo" style="margin-top: 10px;" />
      </template>
    </TodoTable>
  </div>
</template>

<script>
import TodoTable from './TodoTable.vue'

export default {
  components: {
    TodoTable
  },
  data() {
    return {
      search: null,
      form: {
        title: null,
        desc: null
      },
      todos: []
    }
  },
  computed: {
    tableData() {
      if (this.search === null || this.search.trim() === '') return this.todos

      return this.todos.filter(t => t.title.toLowerCase().includes(this.search.toLowerCase()))
    }
  },
  methods: {
    addTodo() {
      this.todos.push(this.form)
      this.clearForm()
    },
    deleteTodo(index) {
      this.todos.splice(index, 1)
    },
    clearForm() {
      this.form = { title: null, desc: null }
    }
  }
}
</script>

<style scoped>
input,
textarea {
  border: 1px solid #DADADA;
  display: block;
  padding: 10px;
  margin-bottom: 16px;
  width: 450px;
  border-radius: 8px;
}

button {
  background-color: #3dacda;
  color: white;
  padding: 8px 16px;
  border: 0;
  border-radius: 8px;
}
</style>