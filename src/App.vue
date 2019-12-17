<template>
  <div class="app">

    <div class="inputBox">
      <textarea placeholder="Your text..." id="inputtext" ></textarea>
      <button type="submit" id="random" @click="getWord">Choose word</button>
    
  
      <div id='words'></div>


    </div>

    <div class="wordBox">
      <p>Guess this word: </p>
      <div class="guessBox">
        <div class="letter" v-for="letter in letters" :key="letter.id">
          {{letter}}
        </div>
      </div>

      <p>Used letters: </p>
      <div id="usedLetter">
      </div>
    </div>
    
    <div class="inputLetter">
      <input id="letterInput" placeholder="Input letter">
      <button type="submit" @click="saveUsedLetter">Check</button>
    </div>

    <div class="lives">
    <p>Lives: </p>
      <div class="square"></div>
      <div class="square"></div>
      <div class="square"></div>
      <div class="square"></div>
      <div class="square"></div>
    </div>

  </div>
</template>


<script>
export default {
  name: 'app',
  data() {
    return {
      words:[],
      letters:[],
      usedLetters:[]
    }
  },

  methods: {

    getWord() {
      //save paragraph to array words
      var inp = document.getElementById('inputtext'); 
      this.words = inp.value.split(/[ .:;?!~,`"&|()<>{}[\]\r\n/\\]+/);
      inp.words = "";
      document.getElementById("words").innerHTML = this.words;

      //choose random word from array
      var randomNumber = Math.floor(Math.random()*this.words.length); 
      if(randomNumber == 0 || this.words[randomNumber].length < 4) {
        randomNumber = randomNumber + 1;
      }
      var randomWord = this.words[randomNumber];
      //alert(randomWord);

      //split word into letters and generate guessing lines
      this.letters = randomWord.split("");
    },

    saveUsedLetter() {
      var data = document.getElementById('letterInput');
      if(data.value.length == 0 || data.value.length > 1) {
        alert("Input a letter!");
      } else{
        this.usedLetters.push(data.value); 
        document.getElementById("usedLetter").innerHTML = this.usedLetters;
      }
    }
  }
};
</script>


<style>
.letter {
  display: inline-block;
  border-bottom: 1px solid;
  margin: 0px 3px 0px 3px;
  font-size: 35px;
  min-width: 30px;
  vertical-align: bottom;
}

.square {
  margin-right: 10px;
  float: left;
  height: 30px;
  width: 30px;
  background-color: #0bd42f;
}
</style>
