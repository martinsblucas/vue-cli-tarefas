<template>
  <div class="task-input">
    <form @submit="addTask($event)">
      <input type="text" class="form-element" name="task" value="" placeholder="Adicione uma tarefa">
      <button type="submit" class="form-element">+</button>
    </form>
  </div>
</template>

<script>
export default {
  methods: {
    addTask($event) {
      $event.preventDefault()

      if ($event.target.task.value) {
        this.$emit('taskAdded', $event.target.task.value)
        $event.target.task.value = ''
      }
    }
  }
}
</script>

<style scoped>
.task-input {
  margin: 35px;
}

.form-element {
  outline: none;
  font-size: 2rem;
  border: 1px solid #FFF;
  padding: 5px 10px 8px;
  color: #FFF;
}

input.form-element {
  width: 500px;
  background: #FFF2;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}

button.form-element {
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  background-color: #2196F3;
}
</style>
