<template>
  <div class="container">
    <b>Budget App</b>
    <div class="row" style="">
      <div class="content">
        despezas
        <div>R$-15000</div>
      </div>
      <div class="content">
        receitas
        <div>R$10000</div>
      </div>
      <div class="content">
        total
        <div>R$4000</div>
      </div>
    </div>
    <div class="transection">
      Transações
      <button class="button-transection" @click="showForm">Nova transação</button>
    </div>

    <div class="form" v-if="hidden === true">
    <form class="form-group">
      <div class="form-group">
        <input type="text" v-model="payments.name" id="name" placeholder="Seu Nome"/>
        <span>{{payments.name}}</span>
      </div>
      <div class="form-group">
        <input type="date" v-model="data" name="" id="date" placeholder="data">
      </div>
      <select v-model="type" id="type">
        <option value="receita">receita</option>
        <option value="despeza">despeza</option>
      </select>
      <div class="form-group">
        <input type="text" name="" v-model="value" id="value" placeholder="valor">
      </div>
      <button type="submit">Enviar</button>
    </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      payments: {
        name: '',
        date: '',
        type: '',
        value: '',
      },
      hidden: false,
      total: [],
    }
  },
  methods: {
    showForm() {
      if(this.hidden == false) {
        this.hidden = true
      } else {
        this.hidden = false
      }
      console.log ("func")
    } 
  },
  name: "App",
  components: {},
};
</script>

<style>
.container {
  border: 1px solid black;
  height: 100vh;
}
b {
  display: flex;
  text-align: center;
  font-size: 30px;
  margin: 30px 30px;
  color: black;
}
.row {
  margin: 30px auto;
  display: flex;
  border: 1px solid black;
  width: 500px;
  height: 100px;
  justify-content: space-between;
  align-items: center;
}
.content {
  margin: 10px;
}
.transection {
  display: flex;
  justify-content: space-between;
  margin: 10px 20px;
  font-size: 50px;
}
.button-transection {
  height: 3em;
  width: 9em;
  border: 1px solid black;
  outline: none;
  border-radius: 10px;
  cursor: pointer;
  background: none;
}
form{
 display: flex;
 flex-direction: row;
 gap: 6px;
}
input{
  margin: 8px 0;
}
select {
  height: 20px;
}

.form {
  border: 1px solid black;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;

}
</style>
