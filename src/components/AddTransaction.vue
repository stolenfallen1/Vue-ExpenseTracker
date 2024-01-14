<template>
  <h3>Add new transactions</h3>
  <form id="form">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text.." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount
        <br />
        (negative - expense, positive - income)
      </label>
      <input type="number" id="amount" placeholder="Enter amount.." />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script>
export default {
  setup() {
    return {};
  },
};
</script>

<style lang="scss" scoped></style>
