<script setup lang="ts">
defineProps({
  cart: Object,
});

const emit = defineEmits(["removeProductToCart"]);
</script>

<template>
  <div class="mb-10 p-10 d-flex flex-row align-items-center product">
    <strong class="flex-fill mr-10">{{ cart.title }}</strong>
    <span class="mr-10">{{ cart.price }}€</span>
    <button @click="emit('removeProductToCart', cart.id)" class="btn btn-danger">Delete</button>
  </div>
</template>

<style lang="scss" scoped>
.product {
  border: var(--border);
  border-radius: var(--border-radius);
  background-color: var(--gray-1);
}
</style>
