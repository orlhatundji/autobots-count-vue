<template>
  <div class="content">
    <h1>Autobots</h1>
    <p class="autobots-count">{{ autobots }}</p>
  </div>
</template>

<script>
import { io } from 'socket.io-client'

export default {
  data() {
    return {
      autobots: 0
    }
  },
  created() {
    const socket = io('http://localhost:3000')
    socket.on('autobotCreated', (autobot) => {
      this.autobots += 1
      console.log('New Autobot created:', autobot)
    })

    fetch('http://localhost:3000/autobots/count')
      .then((response) => response.json())
      .then((data) => {
        this.autobots = data
      })
  }
}
</script>

<style scoped>
.content {
  text-align: center;
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.autobots-count {
  font-size: 20em;
}
</style>
