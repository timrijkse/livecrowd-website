<script setup lang="ts">
import { onMounted, ref } from 'vue'

const messages = ref([])

const handleEnter = () => {
  console.log('enter')
}

onMounted(() => {
  setTimeout(() => {
    messages.value.push({
      text: 'Hello, how can I help you today?',
      side: 'left',
      type: 'whatsapp',
    })
  }, 1000)

  setTimeout(() => {
    messages.value.push({
      text: 'Hello, how can I help you today?',
      side: 'right',
      type: 'livecrowd',
    })
  }, 3000)

  setTimeout(() => {
    messages.value.push({
      text: `Hello, how can <span>I help you</span> today?`,
      side: 'left',
      type: 'dark',
    })
  }, 4000)

  setTimeout(() => {
    messages.value.push({
      text: `Hello, how can <span>I help you</span> today?`,
      side: 'left',
      type: 'blue',
    })
  }, 5000)

  setTimeout(() => {
    messages.value.push({ text: `Hello, how can <span>I help you</span> today?`, side: 'left' })
  }, 7000)
})
</script>

<template>
  <div class="chat-animation">
    <div class="chat-animation-background"></div>

    <div class="chat-animation-content">
      <transition-group name="message">
        <p
          v-for="message in messages"
          :class="`message message-${message.side} message-${message.type}`"
          :key="message.text"
          v-html="message.text"
          @enter="handleEnter"
        ></p>
      </transition-group>
    </div>

    <div class="text">
      <h2>
        Engage<br />
        your<br />
        crowd
      </h2>
      <p>Live support for your events.</p>
    </div>
  </div>
</template>

<style scoped>
.chat-animation {
  position: relative;
  width: 100%;
  max-width: 1080px;
  height: 400px;
  margin: 0 auto;
}

.chat-animation-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(193.83deg, #f4f4f4 9.6%, #e6f2fb 110.1%);
  border-radius: 20px;
  z-index: 1;
}

.chat-animation-content {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  width: 50%;
  height: 400px;
  z-index: 2;
}

.message-left,
.message-right {
  display: block;
  max-width: 50%;
  margin: 16px 0;
  border-radius: 32px;
  padding: 10px 20px;
  background-color: #f0f0f0;
}

.chat-animation-content span {
  text-decoration: underline;
}
.message-right {
  margin-left: auto;
}

.message-whatsapp {
  background: #dcf7c5;
  border-radius: 8px;
  filter: drop-shadow(0px 4px 13px rgba(0, 0, 0, 0.18));
}

.message-livecrowd {
  background-color: #5c94a8;
  color: #fff;
}

.message-dark {
  background-color: #39487b;
  color: #fff;
}

.message-blue {
  background-color: #5a4dfb;
  color: #fff;
}

.message-enter-active,
.message-leave-active {
  transition: all 0.5s ease-out;
}

.message-left.message-enter-active {
  opacity: 0;
  transform: translateX(-16px);
}

.message-left.message-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.message-right.message-enter-active {
  opacity: 0;
  transform: translateX(16px);
}

.message-right.message-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.text {
  position: absolute;
  top: 0;
  left: 50%;
  width: 80%;
  padding: 0 32px;
  z-index: 2;
}

.text h2 {
  font-family: 'Sztos';
  font-style: normal;
  letter-spacing: 0.02em;
  font-size: 180px;
  line-height: 0.8em;
  text-transform: uppercase;

  background: linear-gradient(
    93.54deg,
    #000000 -13.19%,
    #0e084c 1.2%,
    #5f81a4 48.31%,
    #58a6ac 87.39%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-fill-color: transparent;
}
</style>
