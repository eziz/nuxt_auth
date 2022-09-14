<template>
  <p>{{ message }}</p>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  data() {
    return {
      message: "",
    };
  },
  async mounted() {
    try {
      const response = await fetch("http://127.0.0.1:8000/api/user", {
        headers: { "Content-Type": "application/json" },
        credentials: "include",
      });

      const content = await response.json();

      this.message =
        " Hi " +
        content.name +
        "  also, this is your email addres :" +
        content.email +
        "  your registered time :" +
        content.created_at;

      this.$nuxt.$emit("auth", true);
    } catch (e) {
      this.message = "You are not logged in";
      this.$nuxt.$emit("auth", false);
    }
  },
});
</script>
