<template>
  <div id="app">
    <header>
     <img class="logo" src="./assets/Logo_Primary.png" />
     <h1 id="accountNumber">
      <span>
        Account Number:
      </span>
      {{accountNumber}}
     </h1>
    </header>
    <main>
      <MainContainer />
    </main>
  </div>
</template>

<script>
import MainContainer from './components/MainContainer.vue';

export default {
  name: 'App',
  components: {
    MainContainer,
  },
  computed: {
    accountNumber() {
      return this.$store.state.Statement.Transactions[0].AccountNumber;
    },
  },
};
</script>

<style>
body {
  background: linear-gradient(to bottom , #555, #999);
  background-attachment: fixed;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
header {
  background-color: white;
  width: 100%;
  height: 70px;
  margin:  auto;
  padding: 15px;
  display: flex;
  justify-content: space-between;
  position: fixed;
  z-index: 1;
  top: 0;
}
main {
  margin: 100px auto;
  padding: 30px;
  background-color: white;
  width: 80%;
  min-height: 300px;
  border-radius: 5px;
}

img {
  width: 250px;
}

#accountNumber {
  align-self: center;
  white-space: nowrap;
  overflow:hidden;
  font-size: 28px;
}

#balances {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
    border-bottom: 1px solid rgb(222, 222, 222);
  }

.tableMobile {
   display: none;
}

@media only screen and (min-width: 735px) and (max-width: 1068px) {
  #accountNumber {
    font-size: 25px;
  }
  #balances {
    flex-direction: column;
  }
  #balances > h1 {
    font-size: 32px;
  }
}

@media only screen and (max-width: 734px){
  main {
    margin-top: 100px;
    padding: 20px;
    width: 90%;
    min-height: 300px;
    border-radius: 5px;
  }

  #accountNumber {
    font-size: 23px;
  }

  #accountNumber > span {
    display: none;
  }

  #balances {
    flex-direction: column;
  }

  #balances > h1 {
    font-size: 25px;
  }

  #transactions {
    font-size: 25px;
  }

  .tableBigScreen {
    display: none;
  }

  .tableMobile {
    display: inline;
  }
}

</style>
