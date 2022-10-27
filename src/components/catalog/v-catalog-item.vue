<template>
  <div class="v-catalog-item">
    <v-popup
      v-if="isPopupInfoVisible"
      @closePopupInfo="closePopupInfo"
      @rightBtnClickAction="onAddToCart"
      rightBtnTitle="Add To Cart"
      :popupTitle="product_data.name"
    >
      <div>
        <img
          class="v-catalog-item__image"
          :src="require('../../assets/images/' + product_data.image)"
          alt="img"
        />
        <p class="v-catalog-item__name">{{ product_data.name }}</p>
        <p class="v-catalog-item__price">{{ product_data.price }} Р</p>
        <p class="v-catalog-item__price">{{ product_data.category }}</p>
      </div>
    </v-popup>
    <img
      class="v-catalog-item__image"
      :src="require('../../assets/images/' + product_data.image)"
      alt="img"
    />
    <p class="v-catalog-item__name">{{ product_data.name }}</p>
    <p class="v-catalog-item__price">{{ product_data.price }} Р</p>
    <button class="v-catalog-item__show-info" @click="showPopupInfo">
      Show info
    </button>
    <button class="v-catalog-item__add-to-cart-btn btn" @click="onAddToCart">
      Add to Cart
    </button>
  </div>
</template>

<script>
import vPopup from "../popup/v-popup.vue";
export default {
  name: "v-catalog-item",
  components: { vPopup },
  data() {
    return {
      isPopupInfoVisible: false,
    };
  },
  props: {
    product_data: {
      type: Object,
      default() {
        return {};
      },
    },
  },
  methods: {
    onAddToCart() {
      console.log("uhjuih");
      this.$emit("addToCart", this.product_data);
    },
    showPopupInfo() {
      this.isPopupInfoVisible = true;
    },
    closePopupInfo() {
      this.isPopupInfoVisible = false;
    },
  },
};
</script>

<style lang="scss">
.v-catalog-item {
  flex-basis: 25%;
  box-shadow: 0 0 8px 0 #c8c8c8;
  padding: $padding * 2;
  margin-bottom: $margin * 2;
  &__image {
    width: 100px;
  }
}
</style>
