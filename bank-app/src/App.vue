<template>
  <header>Bank App</header>
  <div class="functionBox">
    <!-- 入力画面  -->
    <div class="input">
      <h2>＜入力画面＞</h2>
      <input type="number" v-model="inputMoney" />
      <div class="inputValue">入力額：{{ inputMoney }}円</div>
      <div class="button">
        <button v-on:click="payment" class="buttonItem">入金</button>
        <button v-on:click="withdrawal" class="buttonItem">出金</button>
      </div>
    </div>
    <!-- 口座記録 -->
    <div class="output">
      <h2>＜口座残高＞</h2>
      <div class="balance">残高：{{ balance }}円</div>
    </div>
    <!-- 取引記録 -->
    <div class="transaction">
      <h2>＜取引記録＞</h2>
      <div class="record">
        <div v-for="log in logs" :key="log.id">
          日付：{{ log.date }}<br />
          操作：{{ log.type }}<br />
          金額：{{ log.money }}<br />
          <br />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputMoney: 0,
      balance: 0,
      logs: [],
    };
  },
  methods: {
    payment() {
      this.balance += Number(this.inputMoney);
      this.logs.push({
        date: new Date(),
        type: "入金",
        money: this.inputMoney,
      });
    },
    withdrawal() {
      if (this.balance >= this.inputMoney) {
        this.balance -= Number(this.inputMoney);
        this.logs.push({
          date: new Date(),
          type: "出金",
          money: this.inputMoney,
        });
      }
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  font-family: "SF Pro Text", "SF Pro Icons", "Helvetica Neue", "Helvetica",
    "Arial", sans-serif;
  background-color: #ddd;
}
header {
  margin-top: 20px;
  font-size: 50px;
  text-align: center;
  margin-bottom: 30px;
}
div {
  display: flex;
  flex-direction: column;
}
.functionBox {
  max-width: 1000px;
  display: flex;
  align-items: center;
  background-color: #f6efdb;
  margin: 0 auto;
}
.input {
  display: flex;
  align-items: center;
  width: 800px;
  background-color: #f6efdb;
  padding-bottom: 40px;
}
.input h2 {
  background-color: #f6efdb;
}
input {
  font-size: 20px;
  width: 150px;
  height: 50px;
  text-align: center;
  background-color: white;
}
.inputValue {
  margin: 10px;
  background-color: #f6efdb;
}
.number {
  margin: 30px 0;
}
h2 {
  max-width: 50vw;
}
.button {
  display: flex;
  flex-direction: row;
  width: 400px;
  height: 50px;
  text-align: center;
  display: flex;
  justify-content: space-around;
  background-color: #f6efdb;
}
.buttonItem {
  margin: 20px 0;
  width: 150px;
  height: 50px;
  font-size: 30px;
  background-color: gold;
}
.record {
  border: solid 1px;
  padding: 20px;
}
.output {
  display: flex;
  align-items: center;
  background-color: #f6efdb;
}
.output h2 {
  background-color: #f6efdb;
}
.balance {
  background-color: #f6efdb;
}
.transaction {
  background-color: #f6efdb;
  padding-bottom: 30px;
}
.transaction h2 {
  background-color: #f6efdb;
}
</style>
