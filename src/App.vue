<script setup>
import { reactive } from 'vue';
import Product from './components/Product.vue';

const addToCart = () => {
  cart.count += 1;
};

let cart = reactive({
  count: 0,
});
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
  data() {
    return {
      cart: 0,
    };
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
  },
};
</script>
