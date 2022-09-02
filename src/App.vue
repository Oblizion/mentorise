<template>
  <div class="container">
    <b>Budget App</b>
    <div class="row" style="">
      <div class="content">
        Despezas
        <div class="money">- R${{ this.grandTotal.expenses.toFixed(2) }}</div>
      </div>
      <div class="content">
        Receitas
        <div class="money">R${{ this.grandTotal.recipe.toFixed(2)}}</div>
      </div>
      <div class="content">
        Total
        <div class="money">R${{ this.grandTotal.total.toFixed(2) }}</div>
      </div>
    </div>
    <div class="transection">
      Transações
      <button class="button-transection" @click="showForm">
        Nova transação
      </button>
    </div>

    <div class="form" v-if="hidden === true">
      <form @submit="onSubmit" class="form-group">
        <div class="form-group">
          <input type="text" v-model="name" id="name" placeholder="nome" />
        </div>
        <div class="form-group">
          <input
            type="date"
            v-model="date"
            name=""
            id="date"
            placeholder="data"
          />
        </div>
        <select v-model="type" id="type">
          <option value="receita">receita</option>
          <option value="despeza">despeza</option>
        </select>
        <div class="form-group">
          <input
            type="text"
            name=""
            v-model="value"
            id="value"
            placeholder="valor"
          />
        </div>
        <input type="submit" value="enviar" @click="filter"/>
      </form>
    </div>
    <table>
        <tr v-for="transaction in transactions" :key="transaction">
          <td>
            {{ transaction.type }}
          </td>
          <td>
            {{ transaction.info }}
          </td>
          <td>
            R${{ transaction.value }}
          </td>
          <td>
            {{ transaction.date }}
          </td>
        </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      payments: {
        name: "",
        date: "",
        type: "",
        value: "",
      },
      transactions: [],
      grandTotal: {
        expenses: 0,
        recipe: 0,
        total: 0,
      },
      hidden: false,

    };
  },
  methods: {
    showForm() {
      if (this.hidden == false) {
        this.hidden = true;
      } else {
        this.hidden = false;
      }
    },
    onSubmit(e) {
      e.preventDefault();
      
      const transaction = {
        type: this.name,
        date: this.date,
        info: this.type,
        value: this.value,
      };
      if (this.type == "receita") {
        this.grandTotal.recipe =
          Number(this.grandTotal.recipe) + Number(this.value);
      } else {
        this.grandTotal.expenses =
          Number(this.grandTotal.expenses) + Number(this.value);
      }
      this.grandTotal.total =
        Number(this.grandTotal.recipe) - Number(this.grandTotal.expenses);
      this.transactions.push(transaction);

    },
    
  },

  name: "App",
  components: {},
};
</script>

<style>

table{
  width: 100%;
  height: 20px;
  margin: 5px;
}

tr{
  border: 1px solid black;
  text-align: center; 
  }

td{
  
  width: 20%;
  padding: 8px;
}
.container {
  border: 1px solid black;
  min-height: 100vh;
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
  margin: 40px;
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
form {
  display: flex;
  flex-direction: row;
  gap: 6px;
}
input {
  margin: 8px 0;
}
select {
  height: 24px;
  margin-top: 7px;
}

.form {
  border: 1px solid black;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.money {
  margin-top: 5px;
}
</style>
