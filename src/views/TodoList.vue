<template>
  <div class="todo-list">
    <h1>{{msg}}</h1>
    <div>現在完成 {{numTodo}} 件數</div>
    <div>達成 {{numCompleted}} 件數</div>
    <div>達成率 {{mileStone}}</div>
    <input
      class="new-todo"
      type="text"
      placeholder="輸入新待辦"
      v-model="newTodo"
      @keyup.enter="addTodo()"
    >
    <ul>
      <li v-for="todo in todoList">
        <input type="checkbox" v-model="todo.completed">
        <span
          :style="{color:todo.completed ? 'green' : 'red'}"
          class="todo"
          @click="todo.completed = !todo.completed"
        >{{todo.name}}</span>
        <span @click="deleteTodo(todo)">x</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "todoList",
  data() {
    return {
      msg: "待辦事項",
      newTodo: null,
      todoList: []
    };
  },
  computed: {
    numTodo() {
      return this.todoList.length;
    },
    numCompleted() {
      return this.todoList.filter(x => x.completed).length;
    },
    mileStone() {
      return Math.floor((this.numCompleted / this.numTodo) * 100 || 0);
    }
  },
  methods: {
    addTodo() {
      if (!this.newTodo) {
        alert("Empty");
        return;
      }

      const newTodo = {
        name: this.newTodo,
        completed: false
      };

      this.todoList.push(newTodo);
      this.newTodo = null;
    },
    deleteTodo(todo) {
      const index = this.todoList.indexOf(todo);
      this.todoList.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.new-todo {
  width: 300px;
  font-size: 18px;
  padding: 5px;
}
ul {
  width: 300px;
  margin: 50px auto;
  list-style: none;
}
.todo {
  font-weight: bold;
  font-size: 18px;
  letter-spacing: 1px;
}
</style>
