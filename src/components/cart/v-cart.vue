<template>
  <div class="v-cart">
    <h2>Cart</h2>
    <router-link :to="{ name: 'catalog' }">
      <div class="v-catalog__link_to_cart">Back to Catalog</div>
    </router-link>
    <p v-if="!CART.length">There are no products in cart...</p>
    <div v-for="(item, index) in CART" :key="item.article">
      <v-cart-item
        :cart_item_data="item"
        @deleteFromCart="deleteFromCart(index)"
        @increment="increment(index)"
        @decrement="decrement(index)"
      ></v-cart-item>
    </div>
    <div class="v-cart__total">
      <p class="total__name">Total:</p>
      <p>{{ cartTotalCost }} Р</p>
    </div>
  </div>
</template>

<script>
import vCartItem from "./v-cart-item";
import { mapActions, mapGetters } from "vuex";

export default {
  name: "v-cart",
  components: { vCartItem },
  computed: {
    cartTotalCost() {
      let result = [];
      if (this.CART.length) {
        debugger;
        for (let item of this.CART) {
          result.push(item.price * item.quantity);
        }

        result = result.reduce(function (sum, el) {
          return sum + el;
        });
        return result;
      } else {
        return 0;
      }
    },
    ...mapGetters(["CART"]),
  },
  methods: {
    ...mapActions([
      "DELETE_FROM_CART",
      "INCREMENT_CART_ITEM",
      "DECREMENT_CART_ITEM",
    ]),
    increment(index) {
      this.INCREMENT_CART_ITEM(index);
    },
    decrement(index) {
      this.DECREMENT_CART_ITEM(index);
    },
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index);
    },
  },
};
</script>

<style lang="scss">
.v-cart {
  &__total {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    padding: $padding * 2 $padding * 5;
    display: flex;
    justify-content: center;
    background: $green-bg;
    color: #ffffff;
    font-size: 20px;
  }
  .total__name {
    margin-right: $margin * 2;
  }
}
</style>
