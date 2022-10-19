<template>
  <div class="v-catalog">
    <h1>Catalog</h1>
    <div class="v-catalog__list">
      <div v-for="product in PRODUCTS" :key="product.article">
        <v-catalog-item :product_data="product" @addToCart="addToCart" />
      </div>
    </div>
  </div>
</template>

<script>
import vCatalogItem from "@/components/v-catalog-item.vue";
import { mapGetters, mapActions } from "vuex";

export default {
  name: "v-catalog",
  components: { vCatalogItem },
  data() {
    return {};
  },
  computed: {
    ...mapGetters(["PRODUCTS"]),
  },
  methods: {
    addToCart(product) {
      this.ADD_TO_CART(product);
      console.log(product);
    },
    ...mapActions(["GET_PRODUCTS_FROM_API", "ADD_TO_CART"]),
  },
  mounted() {
    console.log("mounted");
    this.GET_PRODUCTS_FROM_API().then((response) => {
      if (response.data) {
        console.log("data arriived");
      }
    });
  },
};
</script>

<style lang="scss" scoped>
.v-catalog {
  &__list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
  }
}
</style>
