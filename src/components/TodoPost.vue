/* eslint-disable */
<template>
  <div class="todo-item">
    <input
        class="todo-item-check"
        v-model="todo.done"
        type="checkbox"
        @change="$emit('setStatus', todo)"
    >
    <span class="pic"></span>
    <div class="todo-item-title">{{ todo.title }}</div>
    <div class="todo-item-wrapper-right">
      <div class="todo-item-status"
           v-bind:class="{'status-active': todo.status ==='true', 'status-progress' : todo.status === 'false' }">
        {{ todo.status === 'true' ? "Выполнено" : "В работе" }}
      </div>
      <div class="todo-item-date">{{ Intl.DateTimeFormat('ru').format(todo.date) }}</div>
    </div>
  </div>
</template>
<script>
export default {
  name: "TodoPost",
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
}
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 82.25em;
  height: 3.625em;
  border-top: 1px solid #EEEBE9;
}

.todo-item:hover {
  background: #f6f9ff;
}
.pic {
  background: url("../assets/checkbox_false.svg") no-repeat;
  width: 20px;
  height: 20px;
  position: absolute;
  /*left: 136px;*/
  z-index: 1;
  margin: 0 2.9em 0 2.1em;
}
.todo-item-check {
  margin: 0 2.9em 0 2.875em;
  z-index: 2;
  opacity: 0;
}
.todo-item-check:checked ~.pic {
  background: url("../assets/checkbox_true.svg");
  /*left: 132px;*/
  margin: 0 2.9em 0 1.85em;
  width: 30px;
  height: 20px;
  z-index: 1;
}
.todo-item-title {
  margin-right: auto;
}
.todo-item-status{
}
.todo-item-date {
  margin-right: 2em;
}
.todo-item-wrapper-right {
  width: 19em;
  display: flex;
  justify-content: space-between;
}
/* 1039 from left side of the box */
.status-active {
  color: rgba(19, 78, 193, 1);
}
.status-progress {
  color: rgba(248, 155, 17, 1);
}
</style>