<template>
  <div class="v-cart-item">
    <img
      class="v-cart-item__image"
      :src="require('../../assets/images/' + cart_item_data.image)"
      alt="img"
    />
    <div class="v-cart-item__info">
      <p class="v-cart-item__name">{{ cart_item_data.name }}</p>
      <p class="v-cart-item__price">{{ toFix }} P</p>
      <p class="v-cart-item__article">{{ cart_item_data.article }}</p>
    </div>
    <div class="v-cart-item__quantity">
      <p>Qty:</p>
      <span class="quantity__tools">
        <span class="quantity__btn" @click="decrementItem">-</span>
        {{ cart_item_data.quantity }}
        <span class="quantity__btn" @click="incrementItem">+</span>
      </span>
    </div>
    <button class="v-cart-item__btn" @click="deleteFromCart">
      Delete from cart
    </button>
  </div>
</template>

<script>
export default {
  name: "v-cart-item",
  props: {
    cart_item_data: {
      type: Object,
      default() {
        return {};
      },
    },
  },
  data() {
    return {};
  },
  computed: {
    toFix() {
      let value = parseFloat(this.cart_item_data.price);
      return value.toFixed(2);
    },
  },
  methods: {
    decrementItem() {
      this.$emit("decrement");
    },
    incrementItem() {
      this.$emit("increment");
    },
    deleteFromCart() {
      this.$emit("deleteFromCart");
    },
  },
};
</script>

<style lang="scss">
.v-cart-item {
  display: flex;
  flex-wrap: nowrap;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 0 8px 0 #c8c8c8;
  padding: $padding * 2;
  margin-bottom: $margin * 2;
  &__image {
    max-width: 50px;
  }
}

.quantity__btn {
  cursor: pointer;
}
.quantity__tools {
  user-select: none;
}
</style>
