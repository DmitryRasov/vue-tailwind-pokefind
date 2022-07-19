<template>
  <div class="app">
    <modal-window v-model:show="modalOpen" @hideModal="openModal">
      <todo-form @create="createTodo" @close="openModal"></todo-form>
    </modal-window>
    <div class="navigation">
      <div class="navigation-add">
        <h1 class="title">To do list</h1>
        <button @click="openModal" class="btn-add"></button>
      </div>
      <div class="navigation-sort">
        <div class="navigation-sort-wrapper-left">
          <div class="lupa"></div>
          <input v-model="searchParam" type="search" placeholder="Поиск ID, Имени, статуса или даты" class="search">
        </div>
        <div class="navigation-sort-wrapper-right">
          <div>Сортировать по:</div>
          <todo-select
            v-model="selectedSort"
            :options="sortOptions"
          />
        </div>
      </div>
      <div class="navigation-titles">
        <div style="display: block">Описание</div>
        <div style="display: block">Статус</div>
        <div style="display: block">Дата</div>
      </div>
    </div>
    <todo-list
        :todos="searchedTodo"
        @setStatus="changeStatus"
    />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import TodoForm from "@/components/TodoForm";
import ModalWindow from "@/components/ModalWindow";
import TodoSelect from "@/components/TodoSelect";

export default {
  name: 'App',
  components: {
    TodoList, TodoForm, ModalWindow,
    TodoSelect,
  },
  data(){
    return {
      todos: [
        {title: 'Размещение новостей на сайте', done: true, status: 'true', date: "1650575662000", id: 1},
        {title: 'Внедрить wi-fi для читателей', done: false, status: 'false', date: "1648156462000", id: 2},
        {title: 'Отредактировать раздел "Доступная среда"', done: true, status: 'true', date: "1647292462000", id: 3},
        {title: 'Презентация "Информационные технологии"', done: false, status: 'false', date: "1647292462000", id: 4},
        {title: 'Счётчики - внедрить дизайн', done: false, status: 'false', date: "1646774062000", id: 5},
        {title: 'Сверстать новый layout', done: false, status: 'false', date: "1646601262000", id: 6},
        {title: 'Скролл в новостях', done: true, status: 'true', date: "1646082862000", id: 7},
        {title: 'Форма сброса пароля', done: false, status: 'false', date: "1645737262000", id: 8},
        {title: 'Внедрение модуля Chat', done: true, status: 'true', date: "1645305262000", id: 9},
      ],
      modalOpen: false,
      selectedSort: '',
      searchParam: '',
      title: '',
      sortOptions: [
        {value: 'date', name: 'Дата'},
        {value: 'status', name: 'Статус'},
      ],
    }
  },

  methods: {
    createTodo(todo){
      this.todos.push(todo)
    },
    changeStatus(todo){
      if (todo.done === true) {
        todo.status = 'true'
      } else {
        todo.status = 'false'
      }
    },
    openModal(){
      this.modalOpen = !this.modalOpen
    }
  },
  computed: {
    sortTodos(){
      return [...this.todos].sort((todo1, todo2) => {
        return todo1[this.selectedSort]?.localeCompare(todo2[this.selectedSort])
      })
    },
    searchedTodo(){
      return this.sortTodos.filter(todo => todo?.title?.includes(this.searchParam))
    },
  },
  watch: {
    searchParam(newSearch) {
      localStorage.searchParam = newSearch
    },
    selectedSort(newQuery) {
      localStorage.selectedSort = newQuery
    },
  },
  mounted() {
    if (localStorage.bool) {
      this.todos.forEach((todo, index) => {
        todo[index].done = localStorage.bool
      })
    }
    if (localStorage.searchParam) {
      this.searchParam = localStorage.searchParam
    }
    if (localStorage.selectedSort) {
      this.selectedSort = localStorage.selectedSort
    }
  }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  max-width: 1600px;
  max-height: 900px;
  font-family: 'Montserrat', sans-serif;
}
body {
  display: flex;
  justify-content: center;
}
.app {
  margin-top: 3em;
  width: 82.25em;
}
.title {
  font-weight: bolder;
  font-size: 1.5em;
  font-style: normal;
  padding-left: 1.8em;
}
.btn-add {
  width: 4em;
  height: 4em;
  background: url("./assets/Component 336.svg") no-repeat;
  border: none;
  cursor: pointer;
}
.navigation {
  display: flex;
  flex-direction: column;
  width: 82.25em;

}
.navigation-titles {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 1.875em;
  margin-left: 4.5em;
  margin-bottom: 1em;
}
.navigation-titles div:first-child {
  border-left: 1px solid #C4C4C4;
  padding: .7em 0 .7em 1.2em;
}
.navigation-titles div:nth-child(2n) {
  margin-left: auto;
  border-left: 1px solid #C4C4C4;
  padding: .7em 0 .7em 1.2em;
  margin-right: 7.1em;
}
.navigation-titles div:last-child {
  margin-right: 4.8em;
  border-left: 1px solid #C4C4C4;
  padding: .7em 0 .7em 1.2em;
}
.navigation-add {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1em;
}
.navigation-sort {
  display: flex;
  justify-content: space-between;
}
.lupa {
  background: url("assets/lupa.svg") no-repeat;
  height: 1.2em;
  width: 1.2em;
  margin-right: 1em;
}
.search {
  width: 20em;
  border: none;
}
.search:focus {
  outline: none;
}
.search::placeholder {
  color: #C4C4C4;
}
.navigation-sort-wrapper-left {
  display: flex;
  align-items: center;
  padding-left: 2.4em;

}
.navigation-sort-wrapper-right {
  display: flex;
  align-items: center;
}
</style>
