<template>
  <div>
    <form @submit.prevent>
      <h1 class="title">Асинхронность</h1>
      <input
        v-model="input1"
        class="inp"
        type="number"
        placeholder="Введите начальную задержку"
      />
      <input
        v-model="input2"
        class="inp"
        type="number"
        placeholder="Введите интервал"
      />
      <input
        v-model="input3"
        class="inp"
        type="number"
        placeholder="Введите предельное число"
      />
      <button @click="createInput" class="btn">
        <strong>Начать цикл</strong>
      </button>
    </form>
    <div>
      <div><strong>Результат:</strong></div>
      <ul>
        <li v-for="number in numberArray" :key="number">
          {{ number }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input1: null,
      input2: null,
      input3: null,
      inProgress: false,
      numberArray: [],
    };
  },
  methods: {
    createInput() {
      // console.log('pressToStart');
      if (this.inProgress === true || this.input3 < 1) {
        return;
      }

      //   console.log('startInterval');
      this.numberArray = [];
      // this.numberArray.length = 0
      this.inProgress = true;
      let number = 1;
      setTimeout(() => {
        this.numberArray.push(number);
        if (this.input3 === 1) {
          this.inProgress = false;
          return;
        }
        let interval = setInterval(() => {
          number++;
          if (number >= this.input3) {
            clearInterval(interval);
            this.inProgress = false;
          }
          this.numberArray.push(number);
        }, this.input2);
      }, this.input1);
    },
  },
};
</script>

<style lang="scss">
.title {
  text-align: center;
}

.inp {
  display: flex;
  margin: auto;
  margin-top: 10px;
  text-align: center;
}

.btn {
  display: flex;
  margin: auto;
  margin-top: 10px;
  :hover {
    background: red;
  }
}
</style>

//поменять input1 input2 input3 и createInput и визуя
