<template>
  <div class="header">
    <header>
      <h1>Dictionary App</h1>
    </header>
  </div>
  <main>
    <div class="container">
      <div class="card">
        <h2>Find Word</h2>
        <input v-model="inputWord" type="text" name="word" id="" placeholder="Enter Word" /><br />
        <span>Meaning: {{ meaning }} </span>
        <button @click="search">Search</button>
      </div>
    </div>
  </main>
  <router-view />
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue'
import axios from 'axios';
export default defineComponent({
  setup() {
    const inputWord = ref();
    const data = ref();
    const meaning = ref();
    console.log(inputWord);
    const search = async () => {
    const data = await axios.get(`https://api.dictionaryapi.dev/api/v2/entries/en/${inputWord.value}`);
    console.log(data.data[0].meanings[0].definitions[0].definition);
    meaning.value = data.data[0].meanings[0].definitions[0].definition;
   }
    return {
      inputWord,
      search,
      meaning 
    }
  },
})
</script>


<style>
body {
  margin: 0;
  box-sizing: border-box;
}
.header {
  background-color: rgb(51, 192, 192);
  display: flex;
  justify-content: center;
}
.container {
  height: 89vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.card { 
  background-color: rgb(47, 197, 107);
  width: 600px;
  height: 600px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  border: 1px solid;
  border-radius: 20px;
}
span {
  color: white;
  font-size: larger;
}
</style>
