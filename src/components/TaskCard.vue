<template>
  <div class="task-card" :class="stateClass" @click="taskStateChanged()">
    <slot name="title"></slot>
    <span class="close" @click.stop="deleteTask()">X</span>
  </div>
</template>

<script>
export default {
  props: {
    taskKey: {
      type: Number,
      required: true
    },

    task: {
      type: Object,
      required: true
    }
  },

  computed: {
    stateClass() {
      return {
        done: this.task.status,
        pending: !this.task.status
      }
    }
  },

  methods: {
    deleteTask($event) {
      this.$emit('taskDeleted', this.taskKey)
    },

    taskStateChanged() {
      this.$emit('taskStateChanged', this.taskKey)
    }
  }
}
</script>

<style scoped>
.task-card {
  box-sizing: border-box;
  width: 350px;
  height: 150px;
  padding: 10px;
  border-radius: 8px;
  font-size: 2rem;
  font-weight: 300;
  cursor: pointer;
  user-select: none;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.pending {
  border-left: 12px solid #B73229;
  background-color: #F44336;
}

.done {
  color: #DDD;
  border-left: 12px solid #0A8F08;
  background-color: #4CAF08;
  text-decoration: line-through;
}

.pending .close {
  background-color: #B73229;
}

.done .close {
  background-color: #0A8F08;
}

.close {
  position: absolute;
  right: 10px;
  top: 10px;
  font-size: .9rem;
  font-weight: 600;
  border-radius: 10px;
  padding: 5px;
}
</style>
