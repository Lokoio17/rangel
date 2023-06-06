<template>
  <div>
    <h1>Jogo Ímpar ou Par</h1>
    <div id="choice">
      <label for="playerInput">Escolha um número de 1 a 6:</label>
      <input type="number" id="playerInput" v-model="playerNumber" min="1" max="6">
    </div>

    <button id="playButton" @click="playGame">Jogar!</button>

    <div id="result">
      <p class="type">Resultado: {{ result }}</p>
      <p>{{ gameResult }}</p>
      <p v-if="gameResult === 'Você venceu!'">Número escolhido pela máquina: {{ machineNumber }}</p>
      <p v-if="errorMessage">{{ errorMessage }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      playerNumber: null,
      machineNumber: null,
      result: '',
      gameResult: '',
      errorMessage: ''
    };
  },
  methods: {
    generateMachineNumber() {
      return Math.floor(Math.random() * 6) + 1;
    },
    clearResult() {
      this.result = '';
      this.gameResult = '';
      this.machineNumber = null;
    },
    playGame() {
      if (this.playerNumber < 1 || this.playerNumber > 6) {
        this.errorMessage = 'Escolha um número entre 1 e 6.';
        this.clearResult();
        return;
      }

      this.errorMessage = '';
      this.machineNumber = this.generateMachineNumber();
      const total = this.playerNumber + this.machineNumber;
      const isEven = total % 2 === 0;

      if (isEven) {
        this.result = 'Par';
      } else {
        this.result = 'Ímpar';
      }

      if (
        (isEven && this.playerNumber % 2 === 0) ||
        (!isEven && this.playerNumber % 2 !== 0)
      ) {
        this.gameResult = 'Você venceu!';
      } else {
        this.gameResult = 'Você perdeu!';
      }
    }
  }
}
</script>
