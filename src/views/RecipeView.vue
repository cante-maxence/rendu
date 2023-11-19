
<script setup>
import { useRoute } from 'vue-router'
import { onMounted, ref } from 'vue'
import { client } from '@/utils/axios'

const route = useRoute()
const recipe = ref({})

const getRecipe = async () => {
  const response = await client.get(`/recipes/${route.params.id}`)
  return response.data
}

onMounted(async () => {

  recipe.value = await getRecipe()
})
</script>

<template>
  <div class="p-recipe-view">
    <p>recipes</p>
    <p>{{ recipe.recipe_name }}</p>
  </div>
</template>

<style lang="scss"></style>