<script setup lang="ts">
import { ref, reactive } from 'vue'

const message = ref('')

const messages: { timeCreate: Date, message: string }[] = reactive([])

function addMessage(e: KeyboardEvent) {
  e.preventDefault()
  messages.push({ timeCreate: new Date, message: message.value.trim() })
  message.value = ''
}
</script>

<template>
  <div class="main-page">
    <div class="messages">
      <div
        v-for="message in messages"
        :key="message.timeCreate"
        class="message"
      >
        <i>
          {{ message.timeCreate.toLocaleTimeString('ru', { hour: '2-digit', minute: '2-digit', second: '2-digit' }) }}:
        </i>
        {{ message.message }}
      </div>
    </div>
    <textarea
      v-model="message"
      class="message-input"
      @keypress.enter="addMessage($event)"
    ></textarea>
  </div>
</template>

<style scoped lang="sass">
.main-page
  display: flex
  flex-flow: column
  padding: 20px

.messages
  height: calc(100vh - 120px)

.message
  padding: 10px
  border-radius: 3px
  border: 1px solid rgba(blue, .1)
  background: rgba(blue, .05)

.message-input
  width: 100%
  height: 80px
</style>
