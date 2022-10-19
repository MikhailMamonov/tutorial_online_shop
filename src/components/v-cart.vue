<template>
  <div v-if="CART.length" class="v-cart">
    <h2>Cart</h2>
    <div v-for="item in CART" :key="item.article">
      <v-cart-item :cart_item_data="item"></v-cart-item>
    </div>
  </div>
</template>

<script>
import vCartItem from "@/components/v-cart-item";
import { mapGetters } from "vuex";

export default {
  name: "v-cart",
  components: { vCartItem },
  computed: {
    ...mapGetters(["CART"]),
  },
};
</script>

<style lang="scss"></style>
