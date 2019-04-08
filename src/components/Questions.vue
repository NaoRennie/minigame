<template>
  <div class="panel">
    <div class="Panel-head">
      <h3 class="panel-head-title">{{ question }}</h3>
    </div>
    <div class="panel-body">
      <button
        class="btn ui blue button"
        style="margin: 10px"
        @click="onAnswer(btnData[0].correct)"
      >{{ btnData[0].answer}}</button>
      <button
        class="btn ui blue button"
        style="margin: 10px"
        @click="onAnswer(btnData[1].correct)"
      >{{ btnData[1].answer}}</button>
      <button
        class="btn ui blue button"
        style="margin: 10px"
        @click="onAnswer(btnData[2].correct)"
      >{{ btnData[2].answer}}</button>
      <button
        class="btn ui blue button"
        style="margin: 10px"
        @click="onAnswer(btnData[3].correct)"
      >{{ btnData[3].answer}}</button>
    </div>
  </div>
</template>

<script>
const MODE_ADDITION = 1;
const MODE_SUBTRACTION = 2;
export default {
  name: "Questions",
  data() {
    return {
      question: "Here are some questions",
      btnData: [
        { correct: true, answer: 0 },
        { correct: false, answer: 0 },
        { correct: false, answer: 0 },
        { correct: false, answer: 0 }
      ]
    };
  },
  methods: {
    generateQuestion() {
      const firstNumber = this.generateRoundNumber(1, 100);
      const secondNumber = this.generateRoundNumber(1, 100);
      const modeNumber = this.generateRoundNumber(1, 2);

      let correctAnswer = 0;

      switch (modeNumber) {
        case MODE_ADDITION:
          correctAnswer = firstNumber + secondNumber;
          this.question = `${firstNumber} + ${secondNumber} =`;
          break;
        case MODE_SUBTRACTION:
          correctAnswer = firstNumber - secondNumber;
          this.question = `${firstNumber} - ${secondNumber} =`;
          break;
        default:
          correctAnswer = 0;
          this.question = "出題エラーです :/";
      }
      this.btnData[0].answer = this.generateRoundNumber(
        correctAnswer - 10,
        correctAnswer + 10,
        correctAnswer
      );
      this.btnData[0].correct = false;
      this.btnData[1].answer = this.generateRoundNumber(
        correctAnswer - 10,
        correctAnswer + 10,
        correctAnswer
      );
      this.btnData[1].correct = false;
      this.btnData[2].answer = this.generateRoundNumber(
        correctAnswer - 10,
        correctAnswer + 10,
        correctAnswer
      );
      this.btnData[2].correct = false;
      this.btnData[3].answer = this.generateRoundNumber(
        correctAnswer - 10,
        correctAnswer + 10,
        correctAnswer
      );
      this.btnData[3].correct = false;

      const correctButton = this.generateRoundNumber(0, 3);
      this.btnData[correctButton].correct = true;
      this.btnData[correctButton].answer = correctAnswer;
    },
    generateRoundNumber(min, max, except) {
      const rndNumber = Math.round(Math.random() * (max - min) + min);
      if (rndNumber == except) {
        return this.generateRoundNumber(min, max, except);
      }
      return rndNumber;
    },
    onAnswer(isCorrect) {
      this.$emit("answered", isCorrect);
    }
  },
  created() {
    this.generateQuestion();
  }
};
</script>

<style >
.panel {
  padding-top: 20px;
  height: 250px;
  width: 600px;
  background-color: #99ffff;
}
.btn {
  height: 100px;
  width: 100px;
  font-size: 50px;
  cursor: pointer;
}
.panel-head-title {
  font-size: 40px;
  padding-bottom: 20px;
}
.ui.blue.button {
  font-size: 25px;
}
</style>
