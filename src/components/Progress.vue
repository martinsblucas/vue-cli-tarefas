<template>
  <div class="progress">
    <span class="progress-value">{{ percent }}%</span>
    <div class="progress-bar" :style="{width: `${percent}%`}"></div>
  </div>
</template>

<script>
export default {
  props: {
    percent: {
      type: Number,
      default: 0
    }
  }
}
</script>

<style scoped>
.progress {
  position: relative;
  width: 80%;
  border: 1px solid #FFF;
  color: #FFF;
  border-radius: 8px;
  margin-bottom: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.progress-bar {
  position: absolute;
  height: 100%;
  border-radius: 8px;
  background-color: #4CAF50;
  z-index: 0;
  align-self: flex-start;
}

.progress-value {
  z-index: 1;
}
</style>
