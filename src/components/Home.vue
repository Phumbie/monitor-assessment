<template>
  <div class="container">
    <div class="heading">
      <div>
        <h1>Custom CTR Values</h1>
        <p>The sum of all positions must be 100%</p>
      </div>
      <img src="@/assets/cancel.png" alt="cancel" />
    </div>
    <div class="body">
      <Navbar />
      <div class="field-body">
        <Field
          v-for="(i, index) in positions"
          :key="'i' + index"
          :position="index + 1"
          v-model="i.position"
        />
        <AddFieldButton @click="handleNewField" />
      </div>
      <div class="apply-button">
        <ApplyButton />
      </div>
    </div>
  </div>
</template>
<script>
  import Input from "./Input.vue";
  import Field from "./Field.vue";
  import AddFieldButton from "./AddFieldButton.vue";
  import ApplyButton from "./ApplyButton.vue";
  import Navbar from "./Navbar.vue";
  export default {
    components: {
      Input,
      Field,
      AddFieldButton,
      ApplyButton,
      Navbar,
    },
    data: () => ({
      positions: [
        { position: "" },
        { position: "" },
        { position: "" },
        { position: "" },
        { position: "" },
        { position: "" },
      ],
    }),
    methods: {
      handleNewField() {
        console.log("hi");
        console.log(this.positions);
      },
    },
  };
</script>
<style scoped>
  .container {
    width: 90%;
    margin: auto;
    max-width: 30rem;
    padding: 1rem;
  }
  .container .heading {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .container .heading h1 {
    font-size: 1.5rem;
  }
  .container .heading p {
    font-size: 0.85rem;
  }
  .container .heading img {
    height: 1.5rem;
    max-width: 100%;
    cursor: pointer;
  }
  .container .body {
    background-color: #f4f4f4;
    margin-top: 1rem;
  }
  .body .navbar {
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
  .field-body {
    padding: 0.8rem 0.5rem;
    min-height: 35rem;
    max-height: 45rem;
    overflow: auto;
  }
  .apply-button {
    text-align: center;
    padding: 0.5rem;
  }
</style>
