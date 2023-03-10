<script setup>
import { reactive } from 'vue';
import ReviewForm from './ReviewForm.vue';
defineProps({ msg: String, product: String, src: String });
const onSubmitReview = (payload) => {
  review = payload;
};
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img v-bind:src="imageUrl" />
      </div>

      <div>
        <h1 class="series-title">{{ gameSeries }}</h1>
        <h2 class="game-title">{{ title }}</h2>
        <div>
          <h3 class="price">
            {{ price ? price + ' руб.' : 'Недоступно для покупки' }}
          </h3>
        </div>
        <hr />
        <div>
          <p v-if="specialInfo">{{ specialInfo }}</p>
          <p v-else-if="inventory > 10">в наличии</p>
          <p v-else-if="inventory > 0">осталось мало</p>
          <p v-else>закончилась :(</p>
        </div>

        <div
          v-for="game in gameList"
          @click="setShowGame(game.id)"
          class="link-list-item"
        >
          <div
            class="color-circle"
            :class="[game.title === title ? 'active' : null]"
          ></div>
          <div>
            {{ game.title }}
          </div>
        </div>
        <button
          class="button"
          :class="{ disabledButton: !inStock }"
          :disabled="!inStock"
          @click="$emit('addToCart')"
        >
          в корзину
        </button>
        <ul class="details-list">
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <h2 class="inside-box__title">Состав игры:</h2>
        <ul class="inside-box__list">
          <li v-for="inBox in insideBox">{{ inBox }}</li>
        </ul>
      </div>
    </div>
  </div>
  <ReviewForm />
</template>

<script>
export default {
  data() {
    return {
      cart: 0,
      showGame: null,
      gameSeries: 'Неустрашимые',
      gameList: [
        {
          id: '001',
          title: 'Нормандия',
          price: 2790,
          inStock: true,
          inventory: 10,
          onSale: true,
          specialInfo: null,
          imageUrl: './assets/images/game-1.jpg',
          details: [
            'Вид: Для двоих, Карточная, Стратегическая',
            'Возраст: от 14 лет',
          ],
          insideBox: [
            '108 карт',
            '18 квадратов поля',
            '4 кубика',
            '85 жетонов',
            'Книга сценариев',
            'Правила игры',
          ],
        },
        {
          id: '002',
          title: 'Северная Африка',
          price: 2890,
          inStock: true,
          inventory: 150,
          onSale: false,
          specialInfo: null,
          imageUrl: './assets/images/game-2.jpg',
          details: [
            'Вид: Для двоих, Карточная, Стратегическая',
            'Возраст: от 14 лет',
          ],
          insideBox: [
            '22 квадрата поля',
            '42 карты LRDG',
            '3 карты техники LRDG',
            '11 фишек войск LRDG',
            '16 жетонов контроля LRDG',
            '40 итальянских карт',
            '3 итальянские карты техники',
            '10 итальянских фишек войск',
            '16 итальянских жетонов контроля',
            '3 жетона ключевых точек',
            '24 маркера повреждений',
            '4 жетона точек эвакуации',
            '6 жетонов объектов',
            'Жетон инициативы',
            '4 десятигранных кубика',
            'Книга сценариев',
            'Правила игры',
          ],
        },
        {
          id: '003',
          title: 'Reinforcements',
          price: null,
          specialInfo: 'Скоро стартует предзаказ',
          inStock: false,
          inventory: 0,
          onSale: true,
          imageUrl: './assets/images/game-3.jpg',
          details: [
            'Вид: Для двоих, Карточная, Стратегическая',
            'Возраст: от 14 лет',
          ],
          insideBox: [
            '59 карт',
            '150 квадратов поля',
            '32 жетонов',
            '2 Книги сценариев',
            'Правила игры',
          ],
        },
      ],
    };
  },
  methods: {
    setShowGame(id) {
      this.showGame = this.gameList.find((listItem) => listItem.id === id);
    },
  },
  beforeMount() {
    this.ShowGame = this.gameList[0];
  },
  emits: ['addToCart'],
  computed: {
    title() {
      return this.showGame ? this.showGame.title : this.gameList[0].title;
    },
    price() {
      return this.showGame ? this.showGame.price : this.gameList[0].price;
    },
    imageUrl() {
      return this.showGame ? this.showGame.imageUrl : this.gameList[0].imageUrl;
    },
    specialInfo() {
      return this.showGame
        ? this.showGame.specialInfo
        : this.gameList[0].specialInfo;
    },
    inventory() {
      return this.showGame
        ? this.showGame.inventory
        : this.gameList[0].inventory;
    },
    inStock() {
      return this.showGame ? this.showGame.inStock : this.gameList[0].inStock;
    },
    details() {
      return this.showGame ? this.showGame.details : this.gameList[0].details;
    },
    insideBox() {
      return this.showGame
        ? this.showGame.insideBox
        : this.gameList[0].insideBox;
    },
  },
};
</script>
