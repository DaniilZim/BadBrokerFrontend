<template>
  <div>
    <h3>Find best strategy</h3>
    <form @submit.prevent>
      <label>Date from</label>
      <input
        :value="dateFrom1"
        @input="dateFrom1 = $event.target.value"
        class="input-form"
        type="date"
        placeholder="Date from"
      />
      <label>Date to</label>
      <input
        :value="dateTo1"
        @input="dateTo1 = $event.target.value"
        class="input-form"
        type="date"
        placeholder="Date to"
      />
      <label>Money</label>
      <input
        :value="amount1"
        @input="amount1 = $event.target.value"
        class="input-form"
        type="number"
        placeholder="Money"
      />
      <button class="btn" @click="sendForm">Search</button>
    </form>
    <h6 v-show="isErrorShow">{{ errs }}</h6>
    <OutputForm
      v-show="isOutputShow"
      :dateBuy="dateBuy1"
      :dateSell="dateSell1"
      :tool="tool1"
      :revenue="revenue1"
      :rates="rates"
    />
  </div>
</template>

<script>
import axios from "axios";
import OutputForm from "@/components/OutputForm.vue";

export default {
  data() {
    return {
      dateFrom1: "2022-07-27",
      dateTo1: "2022-07-30",
      amount1: 125,
      isOutputShow: false,
      info: null,
      errs: null,
      dateBuy1: "2022-08-02",
      dateSell1: "2022-08-04",
      tool1: "XXX",
      revenue1: 666,
      rates: [],
      isErrorShow: false,
    };
  },
  components: {
    OutputForm,
  },
  props: {
    dateFrom: String,
    dateTo: String,
    amount: Number,
  },
  methods: {
    sendForm() {
      axios
        .get(
          "https://localhost:5001/Exchange/Best?startDate=" +
            this.dateFrom1 +
            "&endDate=" +
            this.dateTo1 +
            "&moneyUsd=" +
            this.amount1
        )
        .then((response) => {
          this.isErrorShow = false;
          this.dateBuy1 = response.data.buyDate;
          this.dateSell1 = response.data.sellDate;
          this.tool1 = response.data.tool;
          this.revenue1 = response.data.revenue;
          this.rates = response.data.rates;

          this.info = response.data;

          this.isOutputShow = true;
        })
        .catch((e) => {
          this.isErrorShow = true;
          this.errs = e.response.data.errmsg;
          this.isOutputShow = false;
        });
    },
  },
};
</script>

<style scoped lang="scss">
div {
  margin: 5px 0 0;
}

form {
  border: 2px solid teal;
}

input {
  align-items: center;
  margin-left: 10px;
  margin-right: 10px;
}

button {
  margin: 5px 10%;
}
</style>
