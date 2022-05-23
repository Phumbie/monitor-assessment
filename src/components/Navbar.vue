<template>
  <div class="navbar">
    <p>UNATRRIBUTED VALUE REMAINING</p>

    <div class="remainder">
      <p class="remainder-value" @click="$emit('handleRemaining')">
        {{ formatRemainder || 100 }}
      </p>
      <p class="symbol">%</p>
    </div>
  </div>
</template>
<script>
  import Input from "./Input.vue";
  export default {
    components: {
      Input,
    },
    props: {
      remainingPositions: {
        default: "",
      },
    },
    computed: {
      formatRemainder() {
        if (this.remainingPositions) {
          let newValue = parseFloat(this.remainingPositions);
          if (Number.isInteger(this.remainingPositions)) {
            return newValue;
          } else {
            if (this.remainingPositions > -10 && this.remainingPositions < 10) {
              return this.remainingPositions.toFixed(2);
            } else {
              return this.remainingPositions.toFixed(1);
            }
          }
        }
      },
    },
  };
</script>
<style scoped>
  .navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.5rem;
    border: 0.3px solid #898992;
  }
  .navbar p {
    font-weight: 600;
    font-size: 0.8rem;
  }
  .remainder {
    display: flex;
    align-items: center;
  }
  .remainder-value {
    border-radius: 15px;
    padding: 0.3rem 0.8rem;
    background-color: white;

    border: none;
    /* width: 4rem; */
    outline: none;
    margin-right: 0.5rem;
    text-align: center;
    cursor: pointer;
  }

  .remainder .symbol {
    background-color: inherit;
  }
</style>
