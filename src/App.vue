<!-- App.vue -->
<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-md-6">
        <h3>EMI Calculator</h3>
        <form @submit.prevent="calculateEMI">
          <div class="form-group">
            <label for="loanAmount">Loan Amount (INR)</label>
            <input type="number" class="form-control" v-model="loanAmount" required />
          </div>
          <div class="form-group">
            <label for="interestRate">Interest Rate (%)</label>
            <input type="number" class="form-control" v-model="interestRate" required />
          </div>
          <div class="form-group">
            <label for="loanTerm">Loan Term (months)</label>
            <input type="number" class="form-control" v-model="loanTerm" required />
          </div>
          <button type="submit" class="btn btn-primary">Calculate EMI</button>
        </form>
      </div>
      <div class="col-md-6" v-if="showResult">
        <h3>EMI Details</h3>
        <p>EMI: {{ emi }}</p>
        <p>Total Interest Payable: {{ totalInterest }}</p>
        <p>Total Amount Payable: {{ totalAmount }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loanAmount: null,
      interestRate: null,
      loanTerm: null,
      showResult: false,
      emi: null,
      totalInterest: null,
      totalAmount: null,
    };
  },
  methods: {
    calculateEMI() {
      const principal = parseFloat(this.loanAmount);
      const rate = parseFloat(this.interestRate) / 100 / 12;
      const term = parseFloat(this.loanTerm);

      const emi =
        (principal * rate * Math.pow(1 + rate, term)) /
        (Math.pow(1 + rate, term) - 1);

      const totalAmount = emi * term;
      const totalInterest = totalAmount - principal;

      this.emi = emi.toFixed(2);
      this.totalInterest = totalInterest.toFixed(2);
      this.totalAmount = totalAmount.toFixed(2);

      this.showResult = true;
    },
  },
};
</script>

<style>
/* Add your custom styles here */
</style>
