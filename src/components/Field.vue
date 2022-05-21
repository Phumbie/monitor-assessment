<template>
  <div class="field-container">
    <p>POSITION {{ position }}</p>
    <Input
      :value="value"
      @input="$emit('input', $event)"
     
    />
  </div>
</template>
<script>
  import Input from "./Input.vue";
  export default {
    components: {
      Input,
    },
    props: {
      position: {
        type: Number,
        default: 1,
        required: true,
      },
      value: {
        type: String,
        default: "",
      },
    },

  };
</script>
<style scoped>
  .field-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: white;
    border-radius: 10px;
    padding: 0.5rem;
    width: 100%;
    margin: 1rem 0;
  }
  .field-container p {
    font-weight: 600;
    font-size: 0.8rem;
  }
</style>
