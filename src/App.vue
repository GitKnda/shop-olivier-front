<script setup>
import TheHeader from "./components/Header.vue";
import TheFooter from "./components/Footer.vue";
import Cart from "./components/Cart/Cart.vue";
import Shop from "./components/Shop/Shop.vue";
import { onMounted, reactive } from "vue";


// récupération des données depuis le fichier products dans data
let products = reactive([]);
const cart = reactive([]);

async function getProducts(){
  try {
    const response = await fetch('http://localhost:5000/');
    let data = await response.json();
    products.splice(0, products.length, ...data);
  } catch (error) {
    console.log(error);
  }
}

async function ajouterPanier(id) {
  const response = await fetch('http://localhost:5000/ajouter', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json' 
    },
    body: JSON.stringify({
      id: id,
    })
  });
  try {
    const data = await response.json();
  } catch (error) {
    
  }

}

onMounted(() => {
  getProducts();
});


function addProductToCart(productId){
  console.log(productId);
  const newProduct = products.find((product) => product.id === productId);
  cart.push(newProduct);
}

function removeProductToCart(cartId){
  console.log(cartId);
  const removeCart = products.delete((cart) => cart.id === cartId);
  cart.push(removeCart);
}
</script>

<template>
  <div class="app-container">
    <TheHeader class="header" />
    <!-- passage du tableau de produit -->
    <Shop :productList="products" class="shop" @add-product-to-cart="addProductToCart" />
    <Cart :cartList="cart" class="cart" />
    <TheFooter class="footer" />
  </div>
</template>

<style lang="scss">
@use "./assets/base.scss" as *;
@use "./assets/debug.scss" as *;

.app-container {
  min-height: 100vh;
  display: grid;
  grid-template-areas: "header header" "shop cart" " footer footer";
  grid-template-columns: 75% 25%;
  grid-template-rows: 48px auto 48px;
}

.header {
  grid-area: header;
}

.shop {
  grid-area: shop;
}

.cart {
  grid-area: cart;
  border-left: var(--border);
  background-color: #fff;
}

.footer {
  grid-area: footer;
}
</style>
