<template>
  <div class="input-container">
    <input
      type="text"
      :style="{ background: background }"
      :disabled="disabled"
      @input="$emit('input', $event.target.value)"
      @keypress="isNumber"
    />
    <p class="symbol">{{ symbol }}</p>
  </div>
</template>
<script>
  export default {
    props: {
      background: {
        type: String,
        default: "#f3f3f3",
        required: false,
      },
      disabled: {
        type: Boolean,
        default: false,
        required: false,
      },
      symbol: {
        type: String,
        default: "%",
      },
      value: {
        type: String,
        default: "",
        required: false,
      },
    },
    methods: {
      isNumber(evt) {
        evt = evt ? evt : window.event;
        let charCode = evt.which ? evt.which : evt.keyCode;
        if (
          charCode != 46 &&
          charCode > 31 &&
          (charCode < 48 || charCode > 57)
        ) {
          evt.preventDefault();
        } else {
          return true;
        }
      },
    },
  };
</script>
<style scoped>
  .input-container {
    display: flex;
    align-items: center;
  }
  input {
    border-radius: 15px;
    padding: 0.3rem 0.5rem;
    border: none;
    width: 4rem;
    outline: none;
    margin-right: 0.5rem;
    text-align: center;
  }
  input:disabled {
    background: inherit !important;
  }
  .symbol {
    font-weight: 600;
  }
</style>
