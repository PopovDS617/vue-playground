<script setup></script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>
    <label for="name">Название:</label>
    <input id="name" v-model="name" />
    <label for="review">Отзыв:</label>
    <textarea id="review" v-model="review"></textarea>
    <label for="rating">Оценка:</label>
    <select id="rating" v-model.number="rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <label for="recommend">Порекомендовали бы друзьям?</label>
    <select id="recommend" v-model="recommend">
      <option>Да</option>
      <option>Нет</option>
    </select>

    <input class="button" type="submit" value="Submit" />
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      review: '',
      rating: null,
    };
  },
  methods: {
    onSubmit() {
      let productReviewdData = {
        name: this.name,
        review: this.review,
        rating: this.rating,
      };
      this.$emit('reviewSubmit', productReviewdData);
      this.name = '';
      this.review = '';
      this.rating = null;
    },
  },
};
</script>
