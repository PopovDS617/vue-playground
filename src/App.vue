<script setup>
import { reactive } from 'vue';
import Product from './components/Product.vue';
import ReviewForm from './components/ReviewForm.vue';

const addToCart = () => {
  cart.count += 1;
};

let cart = reactive({
  count: 0,
});
let review = reactive({});
</script>

<template>
  <div class="nav-bar">
    <h1 class="page-title">Board games for everyone</h1>
  </div>
  <div class="cart">Корзина: {{ cart.count }}</div>
  <Product @addToCart="addToCart" />
</template>

<script>
export default {
  data() {},
};
</script>
