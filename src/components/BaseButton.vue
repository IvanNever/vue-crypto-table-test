<template>
  <button @click="$emit('getData')">Get data</button>
</template>

<script>
export default {
  name: "BaseButton",
};
</script>

<style lang="scss" scoped>
button {
  &,
  &:link,
  &:visited {
    display: block;
    margin: 0 auto;
    margin-top: 8rem;
    padding: 1rem 4rem;
    font-size: 2.4rem;
    font-weight: 700;
    background-color: #f0f0f0;
    border: 2px solid #e3e3e3;
    border-radius: 3px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  &:hover {
    background-color: #f6f6f6;
  }
}
</style>
