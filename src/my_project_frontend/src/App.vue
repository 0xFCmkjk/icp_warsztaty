<script setup>
import { ref } from 'vue';
import { my_project_backend } from 'declarations/my_project_backend/index';
let displayChat = ref('');

async function handleSubmit(e) {
  e.preventDefault();
  const target = e.target;
  const msg = target.querySelector('#msg').value;
  await my_project_backend.save_msg(msg)
  await getChat()
}

async function getChat() {
  displayChat.value = await my_project_backend.get_chat()
}

getChat()
</script>

<template>
  <main class="container mx-auto">
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />
    <form action="#" @submit="handleSubmit">
      <label for="msg">Enter your message: &nbsp;</label>
      <input id="msg" alt="msg" type="text" />
      <button type="submit">Send message</button>
    </form>
    <section id="displayChat">
      <div v-for="msg in displayChat">{{ msg }}</div>
    </section>
  </main>
</template>
