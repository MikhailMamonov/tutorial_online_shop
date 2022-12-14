<template>
  <div class="v-catalog">
    <v-notification :messages="messages"></v-notification>
    <router-link :to="{ name: 'cart' }">
      <div class="v-catalog__link_to_cart">Cart: {{ CART.length }}</div>
    </router-link>
    <h1>Catalog</h1>
    <div class="filters">
      <v-select
        :options="options"
        :selected="selected"
        @select="sortedByCategory"
      ></v-select>
      <div class="range-slider">
        <input
          type="range"
          min="0"
          max="1000"
          step="10"
          v-model.number="minPrice"
          @change="setRangeSlider"
        />
        <input
          type="range"
          min="0"
          max="1000"
          step="10"
          v-model.number="maxPrice"
          @change="setRangeSlider"
        />
      </div>
      <div class="range-values">
        <p>Min: {{ minPrice }}</p>
        <p>Max: {{ maxPrice }}</p>
      </div>
    </div>
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
import vNotification from "./../notifications/v-notification.vue";

import { mapGetters, mapActions } from "vuex";

export default {
  name: "v-catalog",
  components: { vCatalogItem, vSelect, vNotification },
  data() {
    return {
      options: [
        { name: "Все", value: "ALL" },
        { name: "Мужские", value: "м" },
        { name: "Женские", value: "ж" },
      ],
      selected: "Все",
      sortedProducts: [],
      minPrice: 0,
      maxPrice: 1000,
      messages: [],
    };
  },
  computed: {
    ...mapGetters(["PRODUCTS", "CART", "IS_DESKTOP", "SEARCH_VALUE"]),
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
      this.ADD_TO_CART(product).then(() => {
        let timeStamp = Date.now().toLocaleString();
        this.messages.unshift({
          name: "Товар добавлен в корзину",
          icon: "check_circle",
          id: timeStamp,
        });
      });
    },
    sortedByCategory(category) {
      let vm = this;
      this.sortedProducts = this.PRODUCTS;
      this.sortedProducts = this.sortedProducts.filter(function (item) {
        return item.price > vm.minPrice && item.price < vm.maxPrice;
      });
      if (category) {
        this.sortedProducts = this.sortedProducts.filter(function (e) {
          vm.selected = category.name;
          return e.category === category.name;
        });
      }
    },
    setRangeSlider() {
      if (this.minPrice > this.maxPrice) {
        let tmp = this.minPrice;
        this.minPrice = this.maxPrice;
        this.maxPrice = tmp;
      }
      this.sortedByCategory();
    },
    sortedProductsBySearchValue(searchValue) {
      this.sortedProducts = [...this.PRODUCTS];
      if (searchValue) {
        this.sortedProducts = this.sortedProducts.filter(function (item) {
          return item.name.toLowerCase().includes(searchValue.toLowerCase());
        });
      } else {
        this.sortedProducts = this.PRODUCTS;
      }
    },
    ...mapActions(["GET_PRODUCTS_FROM_API", "ADD_TO_CART"]),
  },
  watch: {
    SEARCH_VALUE() {
      this.sortedProductsBySearchValue(this.SEARCH_VALUE);
    },
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API().then((response) => {
      if (response.data) {
        this.sortedByCategory();
        this.sortedProductsBySearchValue(this.SEARCH_VALUE);
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
    top: 100px;
    right: 10px;
    padding: $padding * 2;
    border: solid 1px #aeaeae;
    background: #ffffff;
  }
}

.filters {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.range-slider {
  width: 200px;
  margin: auto 16px;
  text-align: center;
  position: relative;
}

.range-slider svg,
.range-slider input[type="range"] {
  position: absolute;
  left: 0;
  bottom: 0;
}
input[type="range"]::-webkit-slider-thumb {
  z-index: 2;
  position: relative;
  top: 2px;
  margin-top: -7px;
}
</style>
