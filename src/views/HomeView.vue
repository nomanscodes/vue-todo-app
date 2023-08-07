<template>
  <h1 class="heding">Vue Todo App</h1>
  <div class="todo__container">
    <div class="todo__create">
      <label for="todo">Write Todo</label>
      <div class="todo__inputaddBtn">
        <input required type="text" name="todo" v-model="todo" />
        <button @click="handleSubmit" :class="{ hidden: this.toggle }">Add Todo</button>
        <button @click="handelUpdate" v-if="this.toggle">Update</button>
      </div>
    </div>

    <div class="createdTodo__list">
      <div v-for="item in finalTodo" :key="item.id">
        <div class="createdTodo__singleItem">
          <h3 class="editInputBox">{{ item.name }}</h3>
          <span>
            <button @click="handelEdit(item.id)" class="edit__btn">Edit</button>
            <button @click="handleDelete(item.id)" class="delete__btn">Delete</button>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todo: '',
      finalTodo: [],
      toggle: false,
      editedTodoId: ''
    }
  },
  created() {
    const savedTodo = localStorage.getItem('todo')
    let parseTodo = JSON.parse(savedTodo)
    if (parseTodo) {
      this.finalTodo = parseTodo
    }
  },

  methods: {
    handleSubmit() {
      const newTodo = {
        id: this.finalTodo.length + 1,
        name: this.todo
      }
      if (this.todo !== '') {
        this.finalTodo.push(newTodo)
        this.todo = ''
        localStorage.setItem('todo', JSON.stringify(this.finalTodo))
      }
    },

    handleDelete(id) {
      const fiterdData = this.finalTodo.filter((t) => t.id !== id)
      this.finalTodo = fiterdData
      localStorage.setItem('todo', JSON.stringify(fiterdData))
    },

    handelEdit(id) {
      this.toggle = true
      let editedTodo = this.finalTodo.filter((item) => item.id == id)
      this.todo = editedTodo[0].name
      this.editedTodoId = id
    },
    handelUpdate() {
      const index = this.finalTodo.findIndex((obj) => {
        return obj.id === this.editedTodoId
      })

      let upDateObj = {
        id: this.editedTodoId,
        name: this.todo
      }
      if (this.todo !== '') {
        this.finalTodo[index] = upDateObj
        localStorage.setItem('todo', JSON.stringify(this.finalTodo))
        console.log('index', this.finalTodo)
        this.toggle = false
        this.todo = ''
      }
    }
  }
}
</script>

<style lang="scss">
.heding {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px 0px;
  color: azure;
}

.todo__container {
  max-width: 60%;
  margin: auto;
  background-color: rgb(25, 125, 224);
  padding: 30px;

  .todo__create {
    display: flex;
    flex-direction: column;

    label {
      font-size: 18px;
      font-weight: 500;
      color: azure;
      margin-bottom: 10px;
    }
    .todo__inputaddBtn {
      display: flex;
      align-items: center;
      gap: 20px;
      input {
        padding: 10px;
        background-color: cadetblue;
        font-size: 16px;
        font-weight: 500;
        color: rgb(9, 12, 12);
        border: none;
        width: 100%;

        &:focus {
          outline: none;
        }
      }

      button {
        padding: 9px 10px;
        white-space: nowrap;
        border: none;
        background-color: rgb(78, 139, 141);
        color: azure;
        font-size: 18px;
        font-weight: 600;
        cursor: pointer;
      }
    }
  }

  .createdTodo__list {
    margin-top: 40px;
    display: flex;
    flex-direction: column;
    gap: 12px;

    .createdTodo__singleItem {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background-color: rgb(10, 1, 1);
      padding: 10px;
      border-radius: 2px;

      h3 {
        font-size: 20px;
        font-weight: 500;
        color: azure;
      }
      span {
        display: flex;
        align-items: center;
        gap: 10px;
      }

      button {
        font-size: 17px;
        font-weight: 500;
        border: none;
        padding: 3px 8px;
        cursor: pointer;
      }

      .edit__btn {
        background-color: chocolate;
      }

      .delete__btn {
        background-color: rgb(206, 9, 9);
        color: white;
      }
    }
  }
}
.hidden {
  display: none;
}
</style>
