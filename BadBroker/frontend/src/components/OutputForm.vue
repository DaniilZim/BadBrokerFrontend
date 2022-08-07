<template>
  <div>
    <h4>Result</h4>
    <form @submit.prevent>
      <h6>Date buy:</h6>
      <input
        :value="dateBuy"
        class="input-result"
        type="date"
        placeholder="Date buy"
        readonly
      />
      <h6>Date sell:</h6>
      <input
        :value="dateSell"
        class="input-result"
        type="date"
        placeholder="Date sell"
        readonly
      />
      <h6>Tool:</h6>
      <input
        :value="tool"
        class="input-result"
        type="text"
        placeholder="Tool"
        readonly
      />
      <h6>Revenue:</h6>
      <input
        :value="revenue"
        class="input-result"
        type="number"
        placeholder="Revenue"
        readonly
      />
    </form>
    <div class="rates" v-for="rate in rates" :key="rate.date">
      <div class="rate"><strong>Date:</strong>{{ rate.date }}</div>
      <div class="rate"><strong>Rub:</strong>{{ rate.rub }}</div>
      <div class="rate"><strong>Eur:</strong>{{ rate.eur }}</div>
      <div class="rate"><strong>Gbp:</strong>{{ rate.gbp }}</div>
      <div class="rate"><strong>Jpy:</strong>{{ rate.jpy }}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    dateBuy: String,
    dateSell: String,
    tool: String,
    revenue: Number,
    rates: {
      type: Array,
      required: true,
    },
  },
  methods: {},
};
</script>

<style scoped lang="scss">
div {
  margin: 10px 0 0;
  align-content: center;
}

form {
  display: flex;
  flex-direction: row;
}

input {
  margin-left: 10px;
  margin-right: 10px;
}

.rates {
  border: 1px solid teal;
}

.rate {
  display: inline-block;
  margin: 10px;
}
</style>
