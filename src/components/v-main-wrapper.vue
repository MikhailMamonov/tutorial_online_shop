<template>
  <div class="v-main-wrapper">
    <v-header></v-header>
    <div>{{ title }}</div>
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script>
import vHeader from "../layouts/v-header.vue";

export default {
  name: "v-main-wrapper",
  data() {
    return {
      title: "Main Wrapper",
    };
  },
  components: {
    vHeader,
  },
};
</script>

<style lang="scss">
.v-main-wrapper {
  margin: 0 auto;
}
</style>
