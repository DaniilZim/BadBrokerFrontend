<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <InputForm :dateFrom="dateFrom" :dateTo="dateTo" :amount="amount" />
  </div>
</template>

<script>
// @ is an alias to /src
import InputForm from "@/components/InputForm.vue";

export default {
  name: "HomeView",
  data() {
    return {
      dateFrom: "2022-08-03",
      dateTo: "2022-08-05",
      amount: 125,
    };
  },
  components: {
    InputForm,
  },
};
</script>
