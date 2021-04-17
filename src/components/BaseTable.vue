<template>
  <div class="table">
    <div class="table__row table__header">
      <div class="table__item">Stock</div>
      <div class="table__item">Current</div>
      <div class="table__item">Change</div>
    </div>
    <div class="table__row" v-for="row in mockData" :key="row.stocks">
      <div class="table__item">{{ row.stocks }}</div>
      <div class="table__item">{{ row.current }}</div>
      <div class="table__item" :class="row.change < 0 ? 'red' : 'green'">
        {{ row.change >= 0 ? "+" : "" }}{{ row.change }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BaseTable",
  props: {
    mockData: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.table {
  margin: 5rem auto;
  width: 50rem;
  border: 2px solid #e3e3e3;
  border-radius: 3px;

  &__row {
    display: flex;
    justify-content: space-between;
    padding: 1rem 2rem;

    &:not(:last-child) {
      border-bottom: 2px solid #e3e3e3;
    }
  }

  &__header {
    background-color: #f0f0f0;
    font-weight: 700;
  }

  &__item {
    font-size: 2.4rem;
    flex: 1;
    &:nth-child(1) {
      text-align: left;
    }
    &:nth-child(2) {
      text-align: center;
    }
    &:nth-child(3) {
      text-align: end;
    }
  }
}
.red {
  color: #e74c3c;
}
.green {
  color: #2ecc71;
}
</style>
