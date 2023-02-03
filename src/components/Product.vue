<script setup>
defineProps({ msg: String, product: String, src: String });
</script>

<template>
  <div class="cart">Корзина: {{ cart }}</div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img v-bind:src="showGame.imageUrl" />
      </div>

      <div>
        <h1>{{ showGame.title }}</h1>
        <div>
          <p v-if="showGame.inventory > 10">в наличии</p>
          <p v-else-if="showGame.inventory > 0">осталось мало</p>
          <p v-else>закончилась : (</p>
        </div>

        <div
          v-for="game in gameList"
          @click="setShowGame(game.id)"
          class="link-list-item"
        >
          <div class="color-circle"></div>
          <div>
            {{ showGame.title }}
          </div>
          <ul>
            <li v-for="detail in showGame.details">{{ detail }}</li>
          </ul>
        </div>
        <button class="button" @click="addToCart">в корзину</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cart: 0,
      showGame: this.setShowGame.bind(this, '001'),
      gameSerie: 'Неустрашимые',
      gameList: [
        {
          id: '001',
          title: 'Нормандия',
          inStock: true,
          inventory: 100,
          onSale: true,
          imageUrl: './assets/images/game-1.jpg',
          details: [
            'Вид: Для двоих, Карточная, Стратегическая',
            'Возраст: от 14 лет',
            'Размер коробки: 195x280x74 мм',
            'Вес: 0.94 кг',
          ],
        },
        {
          id: '002',
          title: 'Северная Африка',
          inStock: true,
          inventory: 7,
          onSale: false,
          imageUrl: './assets/images/game-2.jpg',
          details: [
            'Вид: Для двоих, Карточная, Стратегическая',
            'Возраст: от 14 лет',
            'Размер коробки: 195x280x74 мм',
            'Вес: 0.94 кг',
          ],
        },
      ],
    };
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    setShowGame(id) {
      this.showGame = this.gameList.find((listItem) => listItem.id === id);
    },
  },
};
</script>
