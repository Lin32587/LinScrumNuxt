<template>
  <div>
    <!-- <div class="mt-12">
      <AppLogo />
    </div> -->
    <nuxt />
  </div>
</template>

<script>
import AppLogo from "~/components/Logo.vue";

export default {
  components: {
    AppLogo
  },
  data() {
    return {
      colors: ["primary", "secondary", "yellow darken-2", "red", "orange"],
      model: 0
    };
  }
};
</script>

<style>
</style>
