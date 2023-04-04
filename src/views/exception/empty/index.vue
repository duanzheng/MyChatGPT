<script setup lang="ts">
import { onMounted, ref } from 'vue'

const text = '系统正在维护中……'
const typedText = ref('')
let currentIndex = 0
const typing = true
const cursorVisible = ref(true)
const typeWriterEffect = () => {
  if (typing) {
    if (currentIndex < text.length) {
      typedText.value += text.charAt(currentIndex)
      currentIndex++
      setTimeout(() => {
        typeWriterEffect()
      }, 200)
    }
    else {
      currentIndex = 0
      typedText.value = ''
      setTimeout(() => {
        typeWriterEffect()
      }, 1000)
    }
  }
}

const cursorBlinkEffect = () => {
  setInterval(() => {
    cursorVisible.value = !cursorVisible.value
  }, 500)
}
onMounted(() => {
  typeWriterEffect()
  cursorBlinkEffect()
})
</script>

<template>
  <div id="app" class="container-self">
    <div class="text">
      <span v-html="typedText" />
      <span v-show="cursorVisible" class="cursor">|</span>
    </div>
  </div>
</template>

  <style scoped>
  .container-self {
    background-color: black;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .text {
    color: white;
    font-size: 24px;
    font-family: "Courier New", monospace;
    white-space: nowrap;
  }

  .cursor {
    color: white;
    animation: blink 1s infinite;
  }

  @keyframes blink {
    0%, 49% {
      opacity: 1;
    }
    50%, 100% {
      opacity: 0;
    }
  }
  </style>
