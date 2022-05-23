<template>
  <button :disabled="disabled">Apply</button>
</template>
<script>
  export default {
    props: {
      disabled: {
        type: Boolean,
        default: true,
        required: false,
      },
    },
  };
</script>
<style scoped>
  button {
    outline: none;
    padding: 0.5rem 1rem;
    border-radius: 15px;
    background-color: #b0b0b6;
    color: white;
    width: 60%;
    margin: auto;
    border: none;
    text-align: center;
    cursor: pointer;
  }

  button:disabled {
    opacity: 0.3;
    cursor: not-allowed;
  }
</style>
