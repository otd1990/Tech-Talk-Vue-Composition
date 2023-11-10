<template>
  <div id="app">
    <h1 class="heading">Random Image Generator</h1>
    <p v-if="message !== ''">
      {{ message }}
    </p>
    <img v-if="imageUrl !== ''" :src="imageUrl" alt="Random" />
    <div class="buttons-container">
      <button class="button-primary" @click="fetchImage">Generate</button>
      <button class="button-secondary" @click="resetImage">Reset</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const startingMessage = "Hit the button below to get started!";
const imageUrl = ref("");
const message = ref(startingMessage);

const fetchImage = async () => {
  const result = await fetch("https://source.unsplash.com/random/300x300");
  const url = result.url;

  imageUrl.value = url;
  message.value = "";
};

const resetImage = () => {
  imageUrl.value = "";
  message.value = startingMessage;
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.buttons-container {
  display: flex;
  justify-content: center;
  width: 100%;
  margin-top: 22px;
  max-width: 300px;
}

button {
  border: none;
  padding: 0.75rem 1rem;
  font-weight: bold;
  font-size: 1rem;
  border-radius: 4px;
  max-width: 105px;
  width: 100%;
  cursor: pointer;
}

button + button {
  margin-left: 4px;
}

.button-primary {
  background: #155f3e;
  color: #f0ffff;
}
</style>
