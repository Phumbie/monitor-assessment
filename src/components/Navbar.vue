<template>
  <div class="navbar">
    <p>UNATRRIBUTED VALUE REMAINING</p>
    <Input background="white" />
  </div>
</template>
<script>
  import Input from "./Input.vue";
  export default {
    components: {
      Input,
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
</style>
