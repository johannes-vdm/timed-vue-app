<template>
  <div id="app">
    <label
      >Enter your number
      <input class="number-generator" type="number" v-model="limit" />
    </label>
    <Numbers :v-model="maxMinHandler" />
  </div>
</template>

<script>
import Numbers from "@/components/Numbers";

export default {
  name: "App",
  components: { Numbers },
  data() {
    return {
      limit: 100,
    };
  },
  computed: {
    // NOTE:
    // As limits cannot be placed inside the html, limit handling had to be done manually.
    // This ensure that the app will not run into serious performance issues.
    maxMinHandler() {
      if (this.limit < 1) {
        return (this.limit = 1);
        // Place info message here
      } else if (this.limit > 2000) {
        return (this.limit = 2000);
        // Place message handler here
      }
    },
    // !NOTE
  },
};
</script>

<style scoped>
/* NOTE added styling for number input with label */
.number-generator {
  margin: 5px;
  padding: 5px;
}
label {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  padding: 0 5px;
}
/* !NOTE */
</style>
