<script setup>
defineProps({
  title: String,
  description: String,
  image: String
})
</script>

<template>
  <div class="c-recipe-card">
    <div class="c-recipe-card__content">
      <img class="c-recipe-card__image" :src="image" alt="">
      <p class="c-recipe-card__title">{{ title }}</p>
      <p class="c-recipe-card__description">{{ description }}</p>
      <RouterLink :to= "`recipes/${id}`">Plus dinfo</RouterLink>
      
    </div>
  </div>
</template>

<style lang="scss">
.c-recipe-card {
  background-color: $white;
  box-shadow: 0 0 31px 0 rgba(0, 0, 0, 0.05);
  border-radius: 10px;

  &__content {
    padding: 20px;
  }

  &__image {
    width: 100%;
    aspect-ratio: 1;
    object-fit: cover;
  }

  &__title {
    font-size: 22px;
    line-height: 1.2;
    color: black;
    &:not(:first-child) {
      margin-top: 10px;
    }
  }

  &__description {
    font-size: 16px;
    color: black;
    line-height: 1.2;
    &:not(:first-child) {
      margin-top: 10px;
    }
  }
}
</style>
