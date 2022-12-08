<template>
  <div>
    <h1 class="title">Таймер</h1>
    <form @submit.prevent>
      
      <input
        v-model="timer1"
        class="inp"
        type="number"
        placeholder="Введите начальную задержку"
      />
      <input
        v-model="timer2"
        class="inp"
        type="number"
        placeholder="Введите интервал"
      />
      <input
        v-model="timer3"
        class="inp"
        type="number"
        placeholder="Введите предельное число"
      />
      <button class="btn" @click="createTimer">Начать цикл</button>
    </form>
    <div>
      <hr class="line"/>
      <div class="result" ><strong>Результат:</strong></div>
      
      <ul>
        <li
          class="list"
          :style="{ backgroundColor: getRandomColor() }"
          v-for="number in numberArray"
          :key="number"
        >
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
      timer1: null,
      timer2: null,
      timer3: null,
      inProgress: false,
      numberArray: [],
    };
  },
  methods: {
    createTimer() {
      // console.log('pressToStart');
      if (this.inProgress === true || this.timer3 < 1) {
        return;
      }

      //   console.log('startInterval');
      this.numberArray = [];
      // this.numberArray.length = 0
      this.inProgress = true;
      let number = 1;
      setTimeout(() => {
        this.numberArray.push(number);
        if (this.timer3 === 1) {
          this.inProgress = false;
          return;
        }
        let interval = setInterval(() => {
          number++;
          if (number >= this.timer3) {
            clearInterval(interval);
            this.inProgress = false;
          }
          this.numberArray.push(number);
        }, this.timer2);
      }, this.timer1);
    },
    getRandomColor() {
      const colors = ["#46211A", "#693D3D", "#BA5536", "#A43820", "#AF4425"];
      const index = Math.floor(Math.random() * colors.length);
      return colors[index];
    },
  },
};
</script>

<style lang="scss">

.title {
  text-align: center;
  font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;

}

.inp {
  width: 18%;
  font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  display: flex;
  margin: auto;
  margin-top: 10px;
  text-align:left;
  border: none;
  border-radius: 5px;
  box-shadow: 0px 0px 5px gray;

}

.btn {
  font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  display: flex;
  color: #ebdcb2;
  background: #af4425;
  border: none;
  border-radius: 5px;
  margin: auto;
  margin-top: 10px;
  box-shadow: 0 0 10px gray;
  cursor: pointer;
  transition: 0.5s ease-in;

}
.btn:hover {
  background: #cd4f2d;

}

 .btn:active{
    transition: 0.5s ease-in-out;
    filter: brightness(70%);

  }

  .line {
    margin-top: 20px;
    margin-bottom: 20px;
  }

.result{
  font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  font-size: 20px;
  text-align: left;
}

.list {
  font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  color: #ebdcb2;
  display: inline-flex;
  justify-content: space-between;
  padding: 5px;
  margin: 10px;
  box-shadow: 0 0 10px gray;
  border-radius: 5px;
}

</style>

