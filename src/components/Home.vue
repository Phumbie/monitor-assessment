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
      <Navbar
        :remainingPositions="remainingPositions"
        @handleRemaining="handleRemainder"
      />
      <div class="field-body">
        <div
          v-for="(i, index) in positions"
          :key="'i' + index"
          class="field-wrapper"
          @mouseenter="handleMouseEnter"
          @mouseleave="handleMouseLeave"
        >
          <div
            class="field-container"
            :class="{ error: handleError(i.position, index) }"
          >
            <p>POSITION {{ index + 1 }}</p>
            <div class="second-section">
              <Input
                v-model="i.position"
                @focusout="handleFocusOut"
                :disabled="handleDisabled(index)"
              />
              <img
                v-if="positions.length > 6"
                src="@/assets/bin.svg"
                alt=""
                @click="removeField(index)"
              />
            </div>
          </div>
          <p class="error-text" v-if="handleError(i.position, index)">
            Must be lower than Position {{ index }}.
          </p>
        </div>
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
      remainingPositions: "",
    }),
    computed: {
      totalPositions() {
        let total = 0;
        this.positions.forEach((item) => {
          total += Number(item.position);
        });
        return total;
      },
      lastFilledPosition() {
        let arrayIndex = 0;
        this.positions.every((item, index) => {
          if (item.position === "") {
            arrayIndex = index - 1;
            return false;
          }
          return true;
        });
        return arrayIndex;
        // for (let i = 0; i < this.positions.length; i++) {
        //   console.log(i, this.positions.length - 1);
        //   if (i == this.positions.length - 1) {
        //     console.log("e don pass");
        //     arrayIndex = this.positions.length - 1;
        //     break;
        //   } else {
        //     if (this.positions[i].position.length > 0) {
        //       arrayIndex = i;
        //     }
        //   }
        // }
        // console.log(arrayIndex);
        // return arrayIndex;
      },
    },
    methods: {
      handleNewField() {
        let lastIndex = this.positions.length - 1;
        if (this.positions[lastIndex].position.length > 0) {
          this.positions.push({
            position: "",
          });
        }
      },
      handleFocusOut() {
        this.remainingPositions = 100 - this.totalPositions;
      },
      handleDisabled(index) {
        if (index !== 0) {
          return !this.positions[index - 1].position.length > 0;
        }
      },
      handleRemainder() {
        if (this.positions[this.positions.length - 1].position.length > 0) {
          this.positions.push({
            position: 100 - this.totalPositions,
          });
        } else {
          this.positions[this.positions.length - 1].position =
            100 - this.totalPositions;
        }
      },
      handleError(currentValue, index) {
        return (
          index !== 0 &&
          this.positions[index - 1].position < Number(currentValue)
        );
      },
      handleMouseEnter(e) {
        this.positions.length > 6 && e.target.classList.add("hover-container");
      },
      handleMouseLeave(e) {
        e.target.classList.remove("hover-container");
      },
      removeField(index) {
        this.positions.length > 6 && this.positions.splice(index, 1);
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
  .field-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: white;
    border-radius: 10px;
    padding: 0.5rem;
    width: 100%;
    cursor: pointer;
    transition: all 0.5s linear;
  }
  .field-wrapper {
    margin: 1rem 0;
  }
  .field-container p {
    font-weight: 600;
    font-size: 0.8rem;
  }
  .error {
    border: 1px solid #c57f72;
  }
  .error-text {
    color: #c57f72;
    font-size: 0.65rem;
    padding-top: 4px;
  }
  .second-section {
    display: flex;
    align-items: center;
  }
  .second-section img {
    height: 1rem;
    cursor: pointer;
    margin-left: 0.4rem;
    display: none;
  }

  .hover-container:hover .second-section img {
    display: block;
  }
</style>
