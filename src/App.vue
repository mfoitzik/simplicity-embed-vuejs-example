<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import { ref } from 'vue'
import {SimplicityEmbed} from '@simplicitywebtools/simplicity-embed-vue/lib'
const seSetup = ref('http://localhost:5500/config.json')
const seRef = ref<HTMLSimplicityEmbedElement | null>(null);
function openSimplicityEmbed() {
  seRef.value?.$el.open()
}
  function closeSimplicityEmbed() {
    seRef.value?.$el.close();
  }
  function sendCommand() {
    const sendObj = {
      "action": "spin"
    }
    seRef.value?.$el.sendMessage(sendObj);
  }
  function changeConfig() {
    seSetup.value = "http://localhost:5500/config2.json";
  }
  function handleSbNotify(event: CustomEvent) {
    console.log("I received a notify event");
    console.log(event.detail);
  }
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
    <div>
        <button type="button" @click="openSimplicityEmbed">Open</button>
      </div>
      <div>
        <button type="button" @click="closeSimplicityEmbed">Close</button>
      </div>
      <div>
        <button type="button" @click="sendCommand">Send Command</button>
      </div>
      <div>
        <button type="button" @click="changeConfig">Change Config</button>
      </div>
    <simplicity-embed
    :setup="seSetup"
    ref="seRef"
    id="simplicity"
    data-icon="heart"
    data-count="7"
    data-color="rgb(245, 241, 5)"
    data-background="rgb(58,85,156)"
    data-heading="Rate Me!"
    @sbnotify="handleSbNotify">
  </simplicity-embed>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
