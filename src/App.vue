<template>
  <Header/>
  <div class="container">
    <Balance :total="total"/>
    <IncomeExpenses/>
    <TransactionsList :transactions="transactions"/>
    <AddTransaction/>
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionsList from "./components/TransactionsList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import {ref, computed} from "vue";


const transactions = ref([
  {id: 1, text: 'Flower', amount: -19.99},
  {id: 2, text: 'Games', amount: -59.99},
]);

const total = computed(()=> {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
});
</script>