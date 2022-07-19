<template>
  <div>
    <todo-post
        v-for="todo in todos"
        :todo="todo"
        :key="todo.id"
        @setStatus="$emit('setStatus', todo)"
    />
  </div>
</template>

<script>
import TodoPost from "@/components/TodoPost";
export default {
  name: "TodoList",
  components: {
    TodoPost
  },
  props: {
    todos: {
      type: Array,
      required: true,
    }
  },
  data() {
    return {

    }
  },
  computed: {
    setStatus(){
      return this.todo.done === false
          ? 'В работе'
          : 'Выполнено'
    }
  }
}
</script>

<style scoped>

</style>