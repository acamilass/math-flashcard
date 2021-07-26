<template>
  <div class="card">
    <div class="card__numbers">
      <div class="first-col">
        <span>{{ firstNumber }} x {{ secondNumber }} = </span>
      </div>

      <div class="second-col">
        <span
          class="res-numbers"
          v-for="item in arrAnswer"
          :key="item"
          v-on:click="setupClick(item)"
        >
          {{ item }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      firstNumber: this.random(),
      secondNumber: this.random(),
      answer: Number,
      ctrlNumber: Number,
      arrAnswer: [],
      isRight: null,
    };
  },
  created() {
    this.randomAnswers();
  },
  name: "Flashcard",
  props: {},
  methods: {
    random() {
      let randomNumber = Math.floor(Math.random() * 11) + 2;
      return randomNumber;
    },

    randomAnswers() {
      this.answer = this.firstNumber * this.secondNumber;

      this.arrAnswer.push(this.answer);

      this.ctrlNumber = this.firstNumber * this.secondNumber;

      for (var i = 0; i < 3; i++) {
        this.ctrlNumber =
          i < 3 ? this.answer + this.random() : this.answer - this.random();
        this.arrAnswer.push(this.ctrlNumber);
      }

      this.shuffle(this.arrAnswer);
    },

    setupClick(value) {
      if (value == this.answer) {
        this.isRight = true;
        this.restart();
      } else {
        this.isRight = false;

        const index = this.arrAnswer.indexOf(value);

        if (index > -1) {
          this.arrAnswer.splice(index, 1);
        }

        return this.arrAnswer;
      }
    },

    shuffle(array) {
      var currentIndex = array.length;
      var temporaryValue;
      var randomIndex;
      // While there remain elements to shuffle...
      while (0 !== currentIndex) {
        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;
        // And swap it with the current element.
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }
      return array;
    },

    restart() {
      this.firstNumber = this.random();
      this.secondNumber = this.random();
      this.answer = this.firstNumber * this.secondNumber;
      this.arrAnswer = [];

      this.randomAnswers();
    },
  },
};
</script>

<style>
.card {
  background-color: #e7dfc6;
  height: 350px;
  width: 950px;
  border-radius: 5px;

  display: flex;
  align-items: center;
  justify-content: center;
}

.card__numbers {
  width: 100%;
  font-size: 6rem;

  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-direction: column;
}

.second-col {
  width: 100%;

  display: flex;
  justify-content: space-evenly;
}

.res-numbers {
  cursor: pointer;
  font-weight: bold;
}

.wrong {
  background-color: #a4031f;
}

.right {
  background-color: #7bc950;
}
</style>