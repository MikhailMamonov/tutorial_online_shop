<template>
  <div class="v-header">
    <router-link :to="{ name: 'main' }"
      ><img src="../assets/logo.png" alt=""
    /></router-link>
    <div class="search-field">
      <input type="text" v-model="searchValue" />
      <button class="search-btn" @click="search(searchValue)">
        <i class="material-icons">search</i>
      </button>
      <button class="search-btn" @click="clearSearchValue()">
        <i class="material-icons">cancel</i>
      </button>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
export default {
  name: "v-header",
  data() {
    return {
      searchValue: "",
    };
  },
  methods: {
    ...mapActions(["SET_SEARCH_VALUE_TO_VUEX"]),
    search(value) {
      this.SET_SEARCH_VALUE_TO_VUEX(value);
      if (this.$route.path !== "/catalog") {
        this.$router.push("/catalog");
      }
    },
    clearSearchValue() {
      this.searchValue = "";
      this.SET_SEARCH_VALUE_TO_VUEX();
      if (this.$route.path !== "/catalog") {
        this.$router.push("/catalog");
      }
    },
  },
};
</script>

<style lang="scss">
.v-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: $green-bg;
  padding: $padding * 2;
  position: fixed;
  width: 100%;
  top: 0;
  left: 0;
  img {
    width: 50px;
  }
  .search-field {
    padding: $padding * 2;
    position: relative;
    right: 200px;
    display: flex;
    justify-content: center;
    align-items: center;
    .search-btn {
      margin-left: 16px;
      background: transparent;
      border: none;
      cursor: pointer;
    }
  }
}
</style>
