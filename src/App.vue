<template>
  <Header/>
  <div class="container">
    <Balance :total="+total"/>
    <IncomeExpenses :income="+income" :expenses="+expenses"/>
    <TransactionsList :transactions="transactions"/>
    <AddTransaction @submitted="transactionSubmittedHandler"/>
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionsList from "./components/TransactionsList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import {ref, computed} from "vue";
import {useToast} from "vue-toastification";

const toast = useToast();

const transactions = ref([
  {id: 1, text: 'Flower', amount: -19.99},
  {id: 2, text: 'Games', amount: -59.99},
  {id: 2, text: 'Games', amount: +1000},
]);

const total = computed(()=> {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0).toFixed(2);
});

const income = computed(() => {
    return transactions.value.filter((transaction) => {return transaction.amount > 0}).reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0).toFixed(2);
})

const expenses = computed(() => {
    return transactions.value.filter((transaction) => {return transaction.amount < 0}).reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0).toFixed(2);
})

const transactionSubmittedHandler = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    ...transactionData
  });

  toast.success('Transaction was added!')
}

const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
}

</script>