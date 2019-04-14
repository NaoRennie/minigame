<template>
  <div class="container">
    <h1 class="text-center">⭐️あたまの体操⭐️</h1>
    <hr>
    <div class="questions-div">
      <transition name="flip" mode="out-in">
        <component :is="mode" @answered="isAnswered($event)" @comfirmed="mode='Questions'"></component>
      </transition>
    </div>
  </div>
</template>

<script>
import Questions from "./components/Questions";
import Answer from "./components/Answer";
export default {
  name: "App",
  data() {
    return {
      mode: "Questions"
    };
  },
  components: {
    Questions,
    Answer
  },
  methods: {
    isAnswered(isCorrect) {
      if (isCorrect) {
        this.mode = "Answer";
      } else {
        this.mode = "Questions";
        alert("残念・・・落ち着いて考えて！");
      }
    }
  }
};
</script>

<style>
.container {
  text-align: center;
}
.text-center {
  padding-top: 20px;
}
.questions-div {
  text-align: -webkit-center;
}
.flip-enter-active {
  animation: flip-in 0.5s ease-out forwards;
}
.flip-leave-active {
  animation: flip-out 0.5s ease-out forwards;
}
@keyframes flip-out {
  from {
    transform: rotateY(0deg);
  }
  to {
    transform: rotateY(90deg);
  }
}

@keyframes flip-in {
  from {
    transform: rotateY(90deg);
  }
  to {
    transform: rotateY(0deg);
  }
}
</style>
