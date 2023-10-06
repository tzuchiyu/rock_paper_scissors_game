<template>
  <div id="app">
    <h1>剪刀石頭布</h1>
    <div class="score">
      <p>你的得分: {{ userScore }}</p>
      <p>電腦的得分: {{ computerScore }}</p>
    </div>
    <button @click="play('🪨')">🪨</button>
    <button @click="play('🖐️')">🖐️</button>
    <button @click="play('✂️')">✂️</button>
    <div v-if="result !== null">
      <h2>結果</h2>
      <p>你選擇了: {{ userChoice }}</p>
      <p>電腦選擇了: {{ computerChoice }}</p>
      <p>{{ result }}</p>
      <button class="reset-button" @click="reset">再玩一次</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      result: null,
      userChoice: null,
      computerChoice: null,
      userScore: 0,
      computerScore: 0,
    };
  },
  methods: {
    play(userChoice) {
      const choices = ['🪨', '🖐️', '✂️'];
      const computerChoice = choices[Math.floor(Math.random() * choices.length)];

      if (userChoice === computerChoice) {
        this.result = '平局！';
      } else if (
        (userChoice === '🪨' && computerChoice === '✂️') ||
        (userChoice === '🖐️' && computerChoice === '🪨') ||
        (userChoice === '✂️' && computerChoice === '🖐️')
      ) {
        this.result = '你贏了！';
        this.userScore++;
      } else {
        this.result = '你輸了！';
        this.computerScore++;
      }

      this.userChoice = userChoice;
      this.computerChoice = computerChoice;
    },
    reset() {
      this.result = null;
      this.userChoice = null;
      this.computerChoice = null;
    },
  },
};
</script>

<style>
  #app {
    font-family: 'Arial', sans-serif;
    text-align: center;
    margin-top: 60px;
  }

  h1 {
    font-size: 2em;
    margin-bottom: 20px;
    color: #333;
  }

  button {
    font-size: 1.5em;
    margin: 10px;
    padding: 10px 20px;
    background-color: #4caf50;
    border: none;
    color: #fff;
    cursor: pointer;
    border-radius: 5px;
  }

  button:hover {
    background-color: #45a049;
  }

  button:focus {
    outline: none;
  }

  button:active {
    transform: translateY(2px);
  }

  .result {
    margin-top: 20px;
  }

  .result h2 {
    font-size: 1.5em;
    margin-bottom: 10px;
    color: #333;
  }

  .result p {
    font-size: 1.2em;
    margin-bottom: 10px;
  }

  .reset-button {
    font-size: 1em;
    padding: 10px 20px;
    background-color: #f44336;
    border: none;
    color: #fff;
    cursor: pointer;
    border-radius: 5px;
    margin-top: 10px;
  }

  .reset-button:hover {
    background-color: #d32f2f;
  }

  
.score {
  font-size: 1.2em;
  margin-bottom: 20px;
}

.score p {
  margin: 5px;
}
</style>
