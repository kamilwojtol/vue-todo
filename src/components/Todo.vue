<template>
  <div class="container">
      <div class="title-wrapper">
        <h1 class="title" v-text="title"></h1>
      </div>
      <div class="todo-wrapper">
        <input class="input" type="text" @keypress="addTask($event)">
        <div class="todo-container">
          <ul class="todo-list">
            <li class="todo-item" v-for="task in tasks" :key="task.id">
              <p class="todo-id">{{ task.id }}</p>
              <input type="text" class="todo-name" v-model="task.name"/>
              <p class="todo-done" @click="task.done = !task.done">{{ doneChecker(task) }}</p>
              <button @click="deleteTask(task)">Delete</button>
            </li>
          </ul>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'Vue Todo',
      tasks: [
        {id: 1,name: 'Find GECK', done: false, },
        {id: 2,name: 'Kill the mutants', done: false, },
        {id: 3,name: 'Find a waterchip', done: true, },
        {id: 4,name: 'Kill Benny', done: true, },
      ]
    }
  },
  methods: {
    doneChecker(task) {
      if (task.done) {
        return '✔️';
      } else {
        return '❌';
      }
    },

    addTask(event) {
      if (event.key == 'Enter' && event.target.input != false) {
        this.tasks.push({id: this.tasks.length + 1, name: event.target.value, done: false})
        event.target.value = '';
      }
    },

    deleteTask(task) {
      this.tasks.splice(task, 1);
    }
  }
}
</script>

<style scoped>

  .container {
    height: 100vh;
  }

  .title-wrapper {
    text-align: center;
  }

  .todo-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .title {
    font-family: 'Mukta', sans-serif;
    font-size: 64px;
    font-weight: 700;
  }

  .input {
    margin-top: 3rem;
    font-family: 'Mukta', sans-serif;
    font-weight: 300;
    font-size: 24px;
    padding: 0.75rem 2rem;
    border: 0px;
    border-bottom: 1px solid #5e5e5e;
  }

  .todo-container {
    margin-top: 3rem;
  }

  .todo-list {
    list-style-type: none;
  }

  .todo-item {
    padding: 1rem;
    border: 1px solid #5e5e5e;
    margin: 0.25rem;
    
    width: 50vw;
    display: flex;
    justify-content: space-between;
    padding: 0.25rem 0.5rem;
    align-items: center;
    flex-direction: row;
  }

  .todo-name {
    font-family: 'Mukta', sans-serif;
    font-size: 20px;
    border: 0px;
    max-width: 600px;
  }

  .todo-done {
    cursor: pointer;
  }
</style>