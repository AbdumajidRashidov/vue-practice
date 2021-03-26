<template>
  <button :class="mode">
    <slot></slot>
  </button>
</template>
<script>
export default {
  props: ["mode"],
};
</script>
<style scoped>
button {
  padding: 0.7rem 1.5rem;
  font-family: inherit;
  background-color: #3a0061;
  border: 1px solid #3a0061;
  color: white;
  cursor: pointer;
  outline: none;
  font-size: 16px;
  border-radius: 80px;
  margin-right: 10px;
}

button:hover,
button:active {
  background-color: #2a0146;
  border-color: #2a0146;
}

.flat {
  background-color: #ffffff;
  color: #3a0061;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #e5c6fa;
}
</style>
