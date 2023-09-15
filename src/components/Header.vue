<template>
  <header class="header">
    <h1>To do list</h1>
    <p>Hour: {{ currentTime }}</p>
    <p class="p-1">Date: {{ currentDate }}</p>
  </header>
</template>

<script>
import { computed, onMounted, ref } from 'vue'
export default {
  name: 'Header',
  setup() {
    const currentTime = ref('')
    const currentDate = ref('')
    const updateDdate = () => {
      const year = new Date().getFullYear()
      const month = new Date().getMonth() + 1
      const date = new Date().getDate()
      currentDate.value = `${date}-${month}-${year}`
    }
    const updateTime = () => {
      const now = new Date()
      const hour = now.getHours()
      const minute = now.getMinutes()
      const second = now.getSeconds()
      currentTime.value = `${hour}:${minute}:${second}`
    }

    onMounted(() => {
      updateTime() // Gọi updateTime lần đầu khi component được mounted
      updateDdate()
      setInterval(updateTime, 1000) 
      setInterval(updateDdate, 60000)
    })

    return {
      currentTime,
      currentDate
    }
  }
}

</script>

<style scoped>
p {
  position: absolute;
  color: #000;
  top: 71px;
}

.p-1 {
  right: 16px;
}

.header {
  background: rgb(220, 212, 212);
  color: #bf5151;
  text-align: center;
  padding: 10px;
}
</style>