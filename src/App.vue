<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <svg width="350" height="260" viewBox="0 0 350 275"
      preserveAspectRatio="xMidYMid meet">
      <defs>
        <radialGradient id="grad1" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
          <stop offset="2%" style="stop-color:rgb(255,255,255);
          stop-opacity:0" />
          <stop offset="100%" style="stop-color:rgb(0,0,0);stop-opacity:0.9" />
        </radialGradient>
      </defs>
      <polyline v-if="strikes > 5 && strikes < 12" points="217,92 218,95 219,97 221,99 223,99 225,98 226,98 227,99 228,98 229,98 232,96 235,95 237,94 238,93 239,92"
      style="fill:none;stroke:black;stroke-width:1" />
      <polyline v-if="strikes >= 12" points="217,99 218,97 219,95 221,93 223,94 225,95 226,93 227,92 228,92 229,92 232,93 235,94 237,96 238,98 239,99"
      style="fill:none;stroke:black;stroke-width:1" />
      <ellipse v-if="strikes > 5"  cx="230" cy="90" rx="22" ry="22" fill="url(#grad1)" />
      <circle v-if="strikes > 5 && strikes < 12" cx="235" cy="85" r="3" stroke="black" stroke-width="1" fill="none" />
      <circle v-if="strikes > 5 && strikes < 12" cx="218" cy="85" r="3" stroke="black" stroke-width="1" fill="none" />

      <line v-if="strikes >= 12"  x1="231" y1="81" x2="238" y2="89" style="stroke:black;fill:none;stroke-width:2px;" />
      <line v-if="strikes >= 12" x1="238" y1="81" x2="231" y2="89" style="stroke:black;fill:none;stroke-width:2px;" />

      <line v-if="strikes >= 12"  x1="215" y1="81" x2="221" y2="89" style="stroke:black;fill:none;stroke-width:2px;" />
      <line v-if="strikes >= 12" x1="221" y1="81" x2="215" y2="89" style="stroke:black;fill:none;stroke-width:2px;" />

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
    </svg>
    <button @click="iterClick()">{{ buttonTxt }}</button>
    <h3>
      {{ strikes }}
    </h3>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      strikes: 0,
      msg: 'New Hangman Game',
      playing: true,
      buttonTxt: "Guess"
    }
  },
  methods : {
    iterClick () {
      if(this.strikes < 11) {
        this.strikes++
      } else if (this.strikes === 11) {
        this.msg = "You Dead!"
        this.playing = false
        this.strikes++
        this.buttonTxt = "Play Agian?"
      } else {
        this.msg = 'New Hangman Game'
        this.strikes = 0
        this.playing = true
        this.buttonTxt = "Guess"
      }
    }
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
