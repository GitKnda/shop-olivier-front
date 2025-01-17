<script setup lang="ts">
import CartProduct from "./CartProduct.vue";

defineProps({
  cartList: Array,
});

const emit = defineEmits(["removeProductToCart"]);
</script>

<template>
  <div>
    <CartProduct v-for="cart of cartList" :cart="cart" @remove-product-to-cart="(cartId) => emit('removeProductToCart', cartId)"/>
  </div>
</template>

<style lang="scss" scoped></style>
