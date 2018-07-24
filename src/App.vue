
<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <div class="gallows">
      <svg width="350" height="260" viewBox="0 0 350 275"
        preserveAspectRatio="xMidYMid meet">
        <!-- Shade reference for the noggin -->
          <defs>
            <radialGradient id="grad1" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
              <stop offset="2%" style="stop-color:rgb(255,255,255);
              stop-opacity:0" />
              <stop offset="100%" style="stop-color:rgb(0,0,0);stop-opacity:0.9" />
            </radialGradient>
          </defs>
        <!-- End shade reference for the noggin -->
        <!-- Smile -->

          <polyline v-if="strikes > 5 && strikes < 12" points="217,92 218,95 219,97 221,99 223,99 225,98 226,98 227,99 228,98 229,98 232,96 235,95 237,94 238,93 239,92"
          style="fill:none;stroke:black;stroke-width:1" />
        <!-- End Smile -->
        <!-- Frown -->
          <polyline v-if="strikes >= 12" points="217,99 218,97 219,95 221,93 223,94 225,95 226,93 227,92 228,92 229,92 232,93 235,94 237,96 238,98 239,99"
          style="fill:none;stroke:black;stroke-width:1" />
        <!-- End Frown -->
        <!-- Head -->
          <ellipse v-if="strikes > 5"  cx="230" cy="90" rx="22" ry="22" fill="url(#grad1)" />
        <!-- End head -->
        <!-- Eyes -->
          <circle v-if="strikes > 5 && strikes < 12" cx="235" cy="85" r="3" stroke="black" stroke-width="1" fill="none" />
          <circle v-if="strikes > 5 && strikes < 12" cx="218" cy="85" r="3" stroke="black" stroke-width="1" fill="none" />
        <!-- End eyes -->
        <!-- Xs for the eyes -->
          <line v-if="strikes >= 12"  x1="231" y1="81" x2="238" y2="89" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes >= 12" x1="238" y1="81" x2="231" y2="89" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes >= 12"  x1="215" y1="81" x2="221" y2="89" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes >= 12" x1="221" y1="81" x2="215" y2="89" style="stroke:black;fill:none;stroke-width:2px;" />
        <!-- end Xs for the eyes -->
        <!-- The gallows -->
          <line v-if="strikes > 0" x1="80" y1="257" x2="260" y2="257" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes > 1" x1="100" y1="257" x2="100" y2="40" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes > 2" x1="100" y1="40" x2="230" y2="40" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes > 3" x1="100" y1="80" x2="130" y2="40" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes > 3" x1="230" y1="40" x2="230" y2="70" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes > 6" x1="230" y1="110" x2="230" y2="170" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes > 7" x1="230" y1="140" x2="250" y2="120" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes > 8" x1="230" y1="140" x2="210" y2="120" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes > 9" x1="230" y1="170" x2="250" y2="200" style="stroke:black;fill:none;stroke-width:2px;" />
          <line v-if="strikes > 10" x1="230" y1="170" x2="210" y2="200" style="stroke:black;fill:none;stroke-width:2px;" />
        <!-- End the gallows -->

      </svg>
    </div>
    <div>
    </div>
    <div class="letter"
        v-for="(letter, index) in wordDisplayLetters"
          :key="'wordArray' + index">{{letter}}</div></br>
    <div  @click="testLetter(letter)"
        class="possibleLetter" :class="strikeThroughClass(letter)"
          v-for="(letter, index) in lettersArr1" :key="'arr1-' + index">
            {{ letter }}
    </div></br>
    <div  @click="testLetter(letter)"
        class ="possibleLetter" :class="strikeThroughClass(letter)"
          v-for="(letter, index) in lettersArr2" :key="'arr2-' + index">
            {{ letter }}
    </div></br>
    <div  @click="testLetter(letter)"
      class="possibleLetter" :class="strikeThroughClass(letter)"
        v-for="(letter, index) in lettersArr3" :key="'arr3-' + index">
          {{ letter }}
    </div></br>
      <div v-if="this.strikes >= 12">
       <h1>You Lose</h1>
       <button @click="reset()"> Play Again?</button>
     </div>
  </div>
</template>
<script>

const wordsArray = require('./words.js')

export default {
  name: 'app',
  data () {
    return {
      strikes: 0,
      msg: 'New Hangman Game',
      playing: true,
      buttonTxt: "Guess",
      word: '',
      wordDisplayLetters: [],
      usedLetters: [],
      wordArray: [],
      lettersArr1: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I'],
      lettersArr2: ['J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R'],
      lettersArr3: ['S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'],
      win: false
    }
  },
  created() {
    this.word = this.getRandomWord()
    this.wordArray = this.word.toUpperCase().split('')
    this.wordDisplayLetters = Array(this.word.length)
  },
  methods: {
    getRandomWord() {
      //Gets random word from words data in words.js
     let index = Math.floor((Math.random() * wordsArray.default.length + 1))
     let word = wordsArray.default[index]
     wordsArray.default.splice(index, 1)
     return word
   },
   testLetter(chosenLetter){
      this.matchNotMatch(chosenLetter)
      if (!this.wordArray.includes(chosenLetter) && !this.usedLetters.includes(chosenLetter)) {
          this.iterClick(chosenLetter)
      }
      this.usedLetters.push(chosenLetter)
    },
    iterClick (letter) {
      if(this.strikes <= 11) {
        this.strikes++
      } else if (this.strikes === 12) {
        this.playing = false
      } else {
        this.strikes = 0
        this.playing = true
      }
    },
    reset(){
      this.word = this.getRandomWord()
      this.wordArray = this.word.toUpperCase().split('')
      this.wordDisplayLetters = Array(this.word.length)
      this.strikes = 0
      this.usedLetters = []
    },
    strikeThroughClass(letter) {
      if (this.usedLetters.includes(letter)){
        return "diagonal-strike"
      }
    },
    matchNotMatch(letter) {
      let match = false
      for (let i = 0; i < this.wordDisplayLetters.length; i++) {
        if (letter === this.wordArray[i]) {
          this.wordDisplayLetters.splice(i, 1, letter)
        }
          match = true
      }
    }
  }
}
</script>

<style>
  #app {
    text-align: center;
    border: solid 2px lightgray;
    border-radius: 2px;
  }
  .flex-container {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .coolNumber {
    padding: 2px;
    margin: 5px;
  }
  .diagonal-strike {
    background: linear-gradient(to left top, transparent 47.75%, currentColor 49.5%, currentColor 50.5%, transparent 52.25%);
    color: dimgrey;
  }
  .letter {
    display: inline-block;
    border-bottom: 1px solid;
    margin: 0px 3px 0px 3px;
    font-size: 30px;
    min-width: 30px;
    vertical-align: bottom;
    color: #000000;
  }
  .possibleLetter {
    display: inline-block;
    margin: 10px 3px 0px 3px;
    font-size: 30px;
    min-width: 30px;
    cursor: pointer;
  }
  button {
    margin-top: 20px;
    padding: 6px 12px;
    border-radius: 4px;
    cursor: pointer;
    font-size: 15px;
  }
  button:hover {
      background-color: #e6e6e6;
      border-color: #adadad;
  }
  .initial-letter {
    display: inline-block;
    border-bottom: 1px solid;
    border-color: #000000;
    margin: 0px 3px 0px 3px;
    font-size: 30px;
    min-width: 30px;
    vertical-align: bottom;
    color: #ffffff;
  }
</style>
