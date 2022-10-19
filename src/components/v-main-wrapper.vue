<template>
  <div class="v-main-wrapper">
    <div>{{ title }}</div>
    <v-catalog />
    <v-cart />
  </div>
</template>

<script>
import vCatalog from "@/components/v-catalog.vue";
import vCart from "@/components/v-cart.vue";
export default {
  name: "v-main-wrapper",
  components: { vCatalog, vCart },
  data() {
    return {
      title: "Main Wrapper",
    };
  },
  mounted() {
    console.log("Hello, I'm alive");
  },
};
</script>

<style lang="scss" scoped>
.v-main-wrapper {
  max-width: 900px;
  margin: 0 auto;
}
</style>
