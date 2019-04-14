<template>
  <div class="answer-panel">
    <h1>正解！！</h1>
    <button class="next-question ui teal button" @click="onNextQuestion">次の問題にチャレンジ!</button>
  </div>
</template>

<script>
export default {
  name: "Answer",
  methods: {
    onNextQuestion() {
      this.$emit("comfirmed");
    }
  }
};
</script>

<style>
.answer-panel {
  padding-top: 80px;
  height: 250px;
  width: 600px;
  background-color: palegreen;
  border-radius: 20px;
}
.next-question {
  cursor: pointer;
}
</style>
