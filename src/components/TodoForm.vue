<template>
  <form @submit.prevent class="wrapper">
    <div class="head-wrapper">
      <h1 class="title-modal">
        Создать новую задачу
      </h1>
      <button
          class="btn-close"
          @click="closeModal"
      >
      </button>
    </div>

    <div class="create-wrapper">
      <p>Описание</p>
      <input
          v-model="todo.title"
          class="input-text"
          type="text"
          placeholder="Введите описание"
      >
      <button
          class="btn"
          @click="createTodo"
      >
        Создать
      </button>
    </div>
  </form>
</template>

<script>
export default {
  name: "TodoForm",
  data() {
    return {
      todo: {
        title: '',
      }
    }
  },
  methods:{
    closeModal(){
      this.$emit('close')
    },
    createTodo(){
      this.todo.date = Date.now().toString()
      this.todo.status = 'false'
      this.todo.done = false
      this.todo.id = Math.random()
      this.$emit('create', this.todo)
      this.todo = {
        title: ''
      }
    }
  }
}
</script>

<style>
.wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}
.title-modal {
  font-weight: bolder;
  font-size: 1.1em;
  font-style: normal;
  margin-right: auto;
}
.btn-close {
  width: 2em;
  height: 2em;
  background: url("../assets/Component 36.svg") no-repeat;
  /*border-radius: 5px;*/
  cursor: pointer;
  /*color: #fff;*/
  border: none;
}
.head-wrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 2.5em 2.5em 0 2.5em;
}
.create-wrapper {
  padding: 0 2.5em 0 2.5em;
  display: flex;
  flex-direction: column;
}
.input-text {
  width: 300px;
  background: #FFFFFF;
  border: 1px solid #DDE2E4;
  border-radius: 8px;
  padding: 0.6875em 11.25em 0.6875em 1em;
}
.input-text::placeholder {
  /*font-size: 0.875em;*/
}
.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  width: 9.5em;
  height: 3em;
  background: #F0F5FF;
  border-radius: 8px;
  border: none;
  color: #314B99;
  font-size: 1.125em;
  font-weight: 400;
  cursor: pointer;
  margin: 30px auto 50px auto;
}
</style>