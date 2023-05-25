<template>
  <div class="app">
    <div class="hour-picker-container">
      <HourPicker />
    </div>
  </div>
</template>

<script>
import HourPicker from './components/HourPicker'

export default {
  name: 'App',
  components: {
    HourPicker
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');

body {
  font-family: 'Roboto', sans-serif;
}

.app {
  padding: 1rem;
}

.hour-picker-container {
  max-width: 300px;
  margin: 0 auto;
}
</style>
