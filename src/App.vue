
<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <p> {{word}} </p>
  </div>
</template>

<script>

import unirest from 'unirest';

export default {
  name: 'app',
  data () {
    return {
      msg: 'New Hangman Game',
      wordBank: ['Hangman', 'Detroit', 'Happiness','Kite','River'],
      index: 0,
      word: ''
    }
  },
  created() {
      this.randomWordApi()
  },
  methods: {
    getRandomWord() {
     let index = Math.floor((Math.random() * this.wordBank.length + 1))

     let word = this.wordBank[index]

     this.wordBank.splice(index, 1)

     return word
   },
    async randomWordApi(){
      fetch('https://wordsapiv1.p.mashape.com/words?random=true', {
        headers: {
          "X-Mashape-Key": "tW0afqvn72mshW26R5qSzD0Ix8g5p19lwqcjsnGKh4XVnyKcHW",
          "Accept": "application/json"
        }
      }).then(res => res.json())
      .then((data) => {this.word = data.word})
    }   
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  font-weight: normal;
}
</style>
