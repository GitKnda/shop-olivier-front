<script setup lang="ts">
import CartProduct from "./CartProduct.vue";

defineProps({
  cartList: Array,
});
</script>

<template>
  <div>
    <CartProduct v-for="cart of cartList" :cart="cart"/>
  </div>
</template>

<style lang="scss" scoped></style>
