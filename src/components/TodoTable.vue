<template>
  <div>
    <slot name="filter">
    </slot>

    <table>
      <thead>
        <tr>
          <th>Title</th>
          <th>Description</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in todos" :key="index">
          <td>{{ todo.title }}</td>
          <td>{{ todo.desc }}</td>
          <td>
            <button @click="remove(index)">Delete</button>
          </td>
        </tr>

        <tr colspan="3" v-if="!todos.length" class="text-center">
          No data available
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true
    }
  },
  methods: {
    remove(todoIndex) {
      this.$emit('delete', todoIndex)
    }
  }
}
</script>

<style scoped>
table {
  margin-top: 24px;
  width: 470px;
  border: 1px solid black;
}

tr th,
tr td {
  border: 1px solid black;
}

.text-center {
  text-align: center;
}
</style>