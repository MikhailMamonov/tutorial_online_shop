<template>
  <div class="v-catalog">
    <router-link :to="{ name: 'cart' }">
      <div class="v-catalog__link_to_cart">Cart: {{ CART.length }}</div>
    </router-link>
    <h1>Catalog</h1>
    <v-select
      :options="options"
      :selected="selected"
      :isExpanded="IS_DESKTOP"
      @select="sortedByCategory"
    ></v-select>
    <div class="v-catalog__list">
      <div v-for="product in filteredProducts" :key="product.article">
        <v-catalog-item :product_data="product" @addToCart="addToCart" />
      </div>
    </div>
  </div>
</template>

<script>
import vCatalogItem from "./v-catalog-item.vue";
import vSelect from "./../v-select.vue";

import { mapGetters, mapActions } from "vuex";

export default {
  name: "v-catalog",
  components: { vCatalogItem, vSelect },
  data() {
    return {
      options: [
        { name: "Все", value: "ALL" },
        { name: "Мужские", value: "м" },
        { name: "Женские", value: "ж" },
      ],
      selected: "Все",
      sortedProducts: [],
    };
  },
  computed: {
    ...mapGetters(["PRODUCTS", "CART", "IS_DESKTOP"]),
    filteredProducts() {
      if (this.sortedProducts.length) {
        return this.sortedProducts;
      } else {
        return this.PRODUCTS;
      }
    },
  },
  methods: {
    addToCart(product) {
      this.ADD_TO_CART(product);
    },
    sortedByCategory(category) {
      this.sortedProducts = [];
      let vm = this;
      this.PRODUCTS.map(function (item) {
        if (category.name === item.category) {
          vm.sortedProducts.push(item);
        }
      });
      this.selected = category.name;
    },
    ...mapActions(["GET_PRODUCTS_FROM_API", "ADD_TO_CART"]),
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API().then((response) => {
      if (response.data) {
        console.log("data arriived");
      }
    });
  },
};
</script>

<style lang="scss">
.v-catalog {
  &__list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
  }
  &__link_to_cart {
    position: fixed;
    top: 80px;
    right: 10px;
    padding: $padding * 2;
    border: solid 1px #aeaeae;
    background: #ffffff;
  }
}
</style>
