<template>
  <div class="container" style="margin-top: 20px">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">SIMPLE TODO APP</h5>
        <div class="row">
          <div class="col-10">
            <input
              type="text"
              class="form-control"
              v-model="todo"
              @keyup.enter="addTodo"
            />
          </div>
          <div class="col-2">
            <button class="btn btn-info" @click="addTodo">ADD</button>
          </div>
        </div>
        <list
          :todoList="todoList"
          @deleteTodo="deleteTodo"
          @markDone="markDone"
        />
        <small>Total Todo: {{ totalTodo }}</small>
      </div>
    </div>
  </div>
</template>

<script>
import List from "./components/List.vue";

export default {
  components: {
    List,
  },
  data() {
    return {
      todo: "",
      todoList: [],
    };
  },
  mounted() {
    let storedTodoList = JSON.parse(localStorage.getItem("todoList"));
    if (storedTodoList) this.todoList = storedTodoList;
  },
  methods: {
    addTodo() {
      if (!this.todo) return;
      this.todoList.unshift({ activity: this.todo, isDone: false });
      this.storeToLocalStorage();
      this.todo = "";
    },
    deleteTodo(todoIndex) {
      this.todoList = this.todoList.filter((item, index) => {
        if (index !== todoIndex) return item;
      });
      this.storeToLocalStorage();
    },
    markDone(todoIndex) {
      this.todoList = this.todoList.filter((item, index) => {
        if (index === todoIndex) {
          item.isDone = !item.isDone;
        }
        return item;
      });
      this.storeToLocalStorage();
    },
    storeToLocalStorage() {
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
  },
  computed: {
    totalTodo() {
      return this.todoList.length;
    },
  },
};
</script>

<style></style>
