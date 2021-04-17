<template>
  <div id="app">
    <BaseButton @getData="getData" />
    <p v-if="loading">Loading... 😴</p>
    <p v-else-if="errorMessage">
      Ooops! Something went wrong! 🙄<br />
      Try it again later...
    </p>
    <BaseTable v-else-if="mockData.length" :mockData="mockData" />
  </div>
</template>

<script>
import BaseButton from "@/components/BaseButton";
import BaseTable from "@/components/BaseTable";
import { payload } from "@/mocData/index.js";
import simulateAsyncReq from "@/plugins/getDataFunc.js";

export default {
  name: "App",
  components: {
    BaseButton,
    BaseTable,
  },
  data() {
    return {
      mockData: [],
      loading: false,
      errorMessage: false,
    };
  },
  methods: {
    async getData() {
      this.mockData = [];
      try {
        this.errorMessage = false;
        this.loading = true;
        const data = await simulateAsyncReq(payload);
        const sortedData = [...data.stocks].sort();
        sortedData.forEach((item) => {
          const index = data.stocks.indexOf(item);
          const stockData = {};
          stockData.stocks = item;
          stockData.current = data.current[index].toFixed(2);
          stockData.change = (data.current[index] - data.start[index]).toFixed(
            2
          );
          this.mockData.push(stockData);
        });
      } catch (e) {
        this.errorMessage = true;
        console.log(e);
      }
      this.loading = false;
    },
  },
};
</script>

<style lang="scss">
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html {
  font-size: 62.5%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
p {
  font-size: 3rem;
  text-align: center;
  margin-top: 5rem;
}
</style>
