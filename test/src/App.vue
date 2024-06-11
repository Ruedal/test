<script setup>
import { RouterLink, RouterView } from 'vue-router';
// import HelloWorld from './components/HelloWorld.vue';
</script>

<template>
  <div id="app">
    <h1>Income and Expense Calendar</h1>
    <vue-cal
      :events="events"
      @day-click="addTransaction"
      default-view="month"
      :disable-views="['years', 'year']"
    />
  </div>
</template>

<script>
import VueCal from 'vue-cal';
import 'vue-cal/dist/vuecal.css';

export default {
  name: 'App',
  components: {
    VueCal,
  },
  data() {
    return {
      events: [
        {
          start: '2024-06-01',
          end: '2024-06-01',
          title: 'Income: $1000',
          content: 'Income: $1000',
          class: 'income',
        },
        {
          start: '2024-06-05',
          end: '2024-06-05',
          title: 'Expense: $200',
          content: 'Expense: $200',
          class: 'expense',
        },
      ],
    };
  },
  methods: {
    addTransaction(date) {
      const amount = prompt(
        'Enter the amount (positive for income, negative for expense):'
      );
      if (amount) {
        const title =
          amount > 0 ? `Income: $${amount}` : `Expense: $${Math.abs(amount)}`;
        const eventClass = amount > 0 ? 'income' : 'expense';
        this.events.push({
          start: date,
          end: date,
          title,
          content: title,
          class: eventClass,
        });
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.income {
  background-color: #d4edda;
  border: 1px solid #c3e6cb;
  color: #155724;
}

.expense {
  background-color: #f8d7da;
  border: 1px solid #f5c6cb;
  color: #721c24;
}
</style>
