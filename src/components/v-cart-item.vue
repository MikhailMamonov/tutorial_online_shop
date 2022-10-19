<template>
  <div class="v-cart-item">
    <img
      class="v-cart-item__image"
      :src="require('../assets/images/' + cart_item_data.image)"
      alt="img"
    />
    <div class="v-cart-item__info">
      <p class="v-cart-item__name">{{ cart_item_data.name }}</p>
      <p class="v-cart-item__price">{{ cart_item_data.price }} P</p>
      <p class="v-cart-item__article">{{ cart_item_data.article }}</p>
    </div>
    <button class="v-cart-item__btn">Delete from cart</button>
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
};
</script>

<style lang="scss" scoped>
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
</style>
