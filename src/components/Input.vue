<template>
  <div class="input-container">
    <div class="input-card">
      <input
        type="number"
        :style="{ background: background }"
        :disabled="disabled"
        v-model="formatValue"
        @focus="inputActive = true"
        @focusout="
          $emit('focusout');
          inputActive = false;
        "
      />
      <p class="unformatted-text" v-if="value.length > 0">
        {{ value }}
      </p>
    </div>
    <p class="symbol">{{ symbol }}</p>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        formattedValue: "",
        unformattedValue: "",
        newValue: "",
        showUnformattedValue: false,
        inputActive: false,
      };
    },
    props: {
      value: {
        default: "",
        type: String,
      },
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
    },
    computed: {
      formatValue: {
        get() {
          if (this.inputActive) {
            return this.value;
          } else {
            let newValue = parseFloat(this.value);
            if (Number.isInteger(newValue)) {
              return newValue;
            } else {
              if (this.value > -10 && this.value < 10) {
                return newValue.toFixed(2);
              } else {
                return newValue.toFixed(1);
              }
            }
          }
        },
        set(modifiedValue) {
          let newValue = parseFloat(modifiedValue);
          if (isNaN(newValue)) {
            newValue = "";
          }
          this.$emit("input", newValue.toString());
        },
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
    background: #b0b0b6;
    cursor: not-allowed;
  }
  .symbol {
    font-weight: 600;
  }
  input[type="number"] {
    -moz-appearance: textfield;
  }
  /* Chrome, Safari, Edge, Opera */
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
  .input-card {
    position: relative;
  }
  .unformatted-text {
    display: none;
    position: absolute;
    right: 0;
    background-color: #fff;
    padding: 4px 8px;
    border-radius: 6px;
    margin-top: 0.5rem;
    z-index: 10;
    box-shadow: 10px 4px 10px 10px rgba(24, 24, 24, 0.05);
  }
  .input-card:hover .unformatted-text {
    display: block;
  }
</style>
