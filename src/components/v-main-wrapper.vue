<template>
  <div class="v-main-wrapper">
    <div>{{ title }}</div>
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script>
export default {
  name: "v-main-wrapper",
  data() {
    return {
      title: "Main Wrapper",
    };
  },
};
</script>

<style lang="scss">
.v-main-wrapper {
  max-width: 900px;
  margin: 0 auto;
}
</style>
