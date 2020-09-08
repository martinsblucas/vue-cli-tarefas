<template>
  <div id="app">
    <h1>Tarefas</h1>

    <Progress :percent="percent"></Progress>

    <TaskInput @taskAdded="addTask($event)"></TaskInput>

    <TasksList :tasks="tasks"
               @taskDeleted="deleteTask($event)"
               @taskStateChanged="taskStateChanged($event)">
    </TasksList>
  </div>
</template>

<script>
import Progress from "./components/Progress";
import TaskInput from "./components/TaskInput";
import TasksList from "./components/TasksList";

export default {
  data() {
    return {
      tasks: [],
    }
  },

  components: {
    Progress,
    TaskInput,
    TasksList
  },

  computed: {
    percent() {
      const tasksCompleted = this.tasks.filter(item => {
        return item.status;
      })

      return (tasksCompleted.length / this.tasks.length) * 100 || 0;
    }
  },

  watch: {
    tasks: {
      //deep monitora as mudanças dentro dos objetos dos array. sem isso, mudar status do item não chama watch
      deep: true,
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      }
    }
  },

  methods: {
    addTask($event) {
      const hasTask = this.tasks.filter(item => {
        return item.title === $event
      })

      hasTask.length === 0 && this.tasks.push({
          title: $event,
          status: false
        });
    },

    deleteTask($event) {
      const index = this.tasks.indexOf(this.tasks[$event])
      index >= 0 && this.tasks.splice(index, 1)
    },

    taskStateChanged($event) {
      this.tasks[$event].status = !this.tasks[$event].status;
    }
  },

  created() {
    const json = localStorage.getItem('tasks')
    this.tasks = JSON.parse(json) || []
  }
}
</script>

<style>
body {
  font-family: 'Lato', sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #FFF;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
}
</style>
