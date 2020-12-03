<template>
    <div class="main">
      <div id="balances">
        <h1>
          Available Balance: {{availableBalance}}
        </h1>
        <h1>
          Projected Balance: {{availableBalance - pendingTransactionsAmount.toFixed(2)}}
        </h1>
      </div>
      <h2 id="transactions">
          Transactions:
      </h2>
      <b-table
        class="tableBigScreen"
        striped hover
        :items="transactions"
        :fields="fields">
      </b-table>
      <b-table
        class="tableMobile"
        striped hover
        :items="transactions"
        :fields="fieldsMobile">
      </b-table>
    </div>
</template>

<script>
import moment from 'moment';
import Vue from 'vue';
import { BootstrapVue, BootstrapVueIcons } from 'bootstrap-vue';
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap-vue/dist/bootstrap-vue.css';

Vue.use(BootstrapVue);
Vue.use(BootstrapVueIcons);

export default {
  // created() {
  //   console.log(this.$store.state.Statement.NotSettled[0].Amount);
  // },
  data() {
    return {
      fields: [
        {
          key: 'TransactionTypeId',
          label: 'Type',
        },
        {
          key: 'TransactionDate',
          label: 'Date',
          sortable: true,
          formatter: (value) => moment(value).format('MMMM Do YYYY, h:mm:ss a'),
        },
        {
          key: 'Amount',
          sortable: true,
        },
        {
          key: 'MerchantName',
          label: 'Merchant',
        },
        {
          key: 'Billed',
          label: 'Pending',
          sortable: true,
          formatter: 'pending',
        },
      ],
      fieldsMobile: [
        {
          key: 'TransactionDate',
          label: 'Date',
          sortable: true,
          formatter: (value) => moment(value).format('MM/DD/YY'),
        },
        {
          key: 'Amount',
          sortable: true,
        },
        {
          key: 'Billed',
          label: 'Pending',
          sortable: true,
          formatter: 'pending',
        },
      ],
    };
  },
  methods: {
    pending(value) {
      return value ? 'No' : 'Yes';
    },
  },
  name: 'MainContainer',
  computed: {
    transactions() {
      return this.$store.state.Statement.Transactions;
    },
    availableBalance() {
      return this.$store.state.Statement.Transactions
        .filter((transaction) => transaction.Billed === true)
        .sort((a, b) => Date.parse(b.TransactionDate) - Date.parse(a.TransactionDate))[0]
        .AvailableBalance;
    },
    pendingTransactionsAmount() {
      let amount = 0;
      for (let i = 0; i < this.$store.state.Statement.NotSettled.length; i += 1) {
        amount += this.$store.state.Statement.NotSettled[i].Amount;
        console.log(this.$store.state.Statement.NotSettled[i].Amount);
      }
      return amount;
    },
  },
};
</script>

<style scoped>
  /* #balances {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
    border-bottom: 1px solid rgb(222, 222, 222);
  } */
</style>
