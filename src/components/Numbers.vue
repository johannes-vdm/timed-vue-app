<template>
  <div>
    <div
      class="number"
      :id="'number-' + number"
      v-for="number in n()"
      :key="number"
      @mouseover="hov(number)"
      @mouseout="reset"
    >
      {{ number }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      limit: this.$parent.limit,
      numbers: [],
    };
  },
  watch: {
    ["$parent.limit"](newLimit) {
      this.limit = newLimit;
    },
  },
  methods: {
    n() {
      let numbers = [];
      // NOTE:
      // Using let instead of var, as globilization is not required, nor is it good practice.
      // Numbers should be displayed from 1 - 100 rather than 0 - 100
      // var i = 0; i < this.limit; i++
      // Changed to:
      // let i = 1; i <= this.limit; i++
      for (let i = 1; i <= this.limit; i++) {
        // !NOTE
        numbers = [...numbers, i];
      }
      return numbers.sort(() => Math.random() - 0.5);
    },
    hov(number) {
      const nums = document.querySelectorAll(".number");

      for (let i = 0; i < nums.length; i++) {
        const num = nums[i].textContent.trim();
        if (number % num === 0) {
          nums[i].classList.add("active");
          console.log("divisor", num);
        }
      }
    },
    reset() {
      const nums = document.querySelectorAll(".number");
      nums.forEach((num) => num.classList.remove("active"));
    },
  },
};
</script>

<style scoped>
.number {
  display: inline-block;
  background-color: lightgrey;
  /**
  * NOTE Used for responsivness across platforms,
  * if number space exceed the width of the div,
  * the container will remain the inital amount and the number will break into the next line
  */
  width: 2.4em;
  padding: 0.5em;
  margin: 0.5em;
  text-align: center;
  word-wrap: break-word;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  /* !NOTE */
}

.active {
  background-color: red;
}

/* NOTE Cursor change on hover from typing style*/
.active:hover {
  cursor: crosshair;
  /* !NOTE */
}
</style>