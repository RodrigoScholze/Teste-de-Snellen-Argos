<template>
  <div id="app">
    <GuidelinesSnellen v-if="SnellenBool == false"/>
    <Snellen v-if="SnellenBool"/>

    <div id="containerButton">
      <button id="StartButton" v-if="SnellenBool == false" @click="SnellenBool = true">Começar</button>
    </div>
  </div>
</template>

<script>
import GuidelinesSnellen from './components/GuidelinesSnellen.vue'
import Snellen from './components/Snellen.vue'

export default {
  name: 'App',
  components: {
    'GuidelinesSnellen': GuidelinesSnellen,
    'Snellen': Snellen
  },
  data(){
    return {
      SnellenBool: false
    }
  },
}
</script>

<style scoped>
@import '/assets/css/normalize.css';
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap');
#containerButton{
  position: absolute;
  bottom: 0px;
  width: 100%;
  text-align: center;
  margin-bottom: 30px;
}
#StartButton{
  font-family: 'Montserrat', sans-serif;
  font-weight: 500;
  background-color: #5551A6;
  border: none;
  border-radius: 32px;
  color: white;
  padding: 8px 12px;
  font-size: 22px;
  width: 450px;
  cursor: pointer;
}
</style>