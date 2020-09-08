<template>
  <div class="tasks-list">
    <template v-if="tasks.length">
      <TaskCard v-for="(task, taskKey) in tasks"
                :key="taskKey"
                :task-key="taskKey"
                :task="task"
                @taskDeleted="taskDeleted($event)"
                @taskStateChanged="taskStateChanged($event)">
      <span slot="title">
        {{ task.title }}
      </span>
      </TaskCard>
    </template>
    <p v-else class="no-task">Adicione uma tarefa</p>
  </div>
</template>

<script>
import TaskCard from "./TaskCard";

export default {
  props: {
    tasks: {
      Array,
      required: true
    }
  },

  components: {
    TaskCard
  },

  methods: {
    taskDeleted($event) {
      this.$emit('taskDeleted', $event)
    },

    taskStateChanged($event) {
      this.$emit('taskStateChanged', $event)
    }
  }
}
</script>

<style>
.tasks-list {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.tasks-list .task-card {
  margin: 10px;
}

.no-task {
  color: #AAA;
  font-size: 1.7rem;
}
</style>
