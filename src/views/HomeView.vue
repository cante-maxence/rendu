<script setup>
import MyButton from '@/components/elements/MyButton.vue'
import DefaultLayout from '@/components/layouts/DefaultLayout.vue'
import MyBackgroundScroll from '@/components/MyBackgroundScroll.vue'
import {computed, onMounted, ref} from "vue"
import RecipeCard from "@/components/RecipeCard/RecipeCard.vue";
import {client} from '@/utils/axios.js'



const recipes = ref([])

const getRecipes = async () => {
  const response = await client.get('/recipes')
  return response.data
}



const recipesNames = computed(() => {
  return recipes.value.map((item) => item.recipe_name)
})

const pizzaRecipes = computed(() => {
  return recipes.value.filter((item) => item.recipe_name.toLowerCase().includes('pizza'))
})



const hasGoalId1 = computed(() => {
  return recipes.value.some((item) => item.goal_id === 1)
})

const addRecipe = () => {
  recipes.value.push({ recipe_name: 'Pizza' })
}

const recipesInHero = 4

const gridPage = ref(1)

const gridRecipes = computed(() => {
  const recipesByPage = 4

  return recipes.value.slice(recipesInHero, recipesInHero + gridPage.value * recipesByPage)
})


const moreRecipesToShow = computed(() => {
  return gridRecipes.value.length < (recipes.value.length - recipesInHero)
})

const seeMoreRecipe = () => {
  gridPage.value++
}

onMounted(async () => {
  recipes.value = await getRecipes()
})
</script>

<template>
  <DefaultLayout>
    <template #header>
      <nav>
        <ul>
          <li><a href="#">Nav link 1</a></li>
          <li><a href="#">Nav link 2</a></li>
          <li><a href="#">Nav link 3</a></li>
        </ul>
      </nav>
    </template>

    <template #aside>
      <img style='max-width: 100px;' src='@/assets/image-1.png' />
      <nav>
        <ul>
          <li><a href="#">Aside link 1</a></li>
          <li><a href="#">Aside link 2</a></li>
          <li><a href="#">Aside link 3</a></li>
        </ul>
      </nav>
    </template>
    <p>Recettes de la grille</p>
    <div class="recipes-list">
      <div v-for="(recipe, index) in gridRecipes" :key="index">
        <RecipeCard :id="recipe.recipe_id" :title="recipe.recipe_name" :description="recipe.recipe_description" :image="recipe.image_url" />
      </div>
    </div>
    <button v-if="moreRecipesToShow" @click="seeMoreRecipe">Voir plus de recettes</button>

    <p>Toutes les recettes</p>
    <div class="recipes-list">
      <div v-for="(recipe, index) in recipes" :key="index">
        <RecipeCard :id="recipe.recipe_id" :title="recipe.recipe_name" :description="recipe.recipe_description" :image="recipe.image_url" />
      </div>
    </div>
    recipes names : {{ recipesNames }} <br><br>
    pizzaRecipes : {{ pizzaRecipes }} <br><br>
    hasGoalId1 : {{ hasGoalId1 }} <br><br>
    <button @click="addRecipe">Ajouter une recette</button>
    <MyBackgroundScroll />

    <template #footer>
      <MyButton href="/about" variant="rounded">My link Button</MyButton>
    </template>
  </DefaultLayout>

  <!-- <MyButton size="small" href="/about">My Small Button</MyButton>
  <MyButton href="/about">My link Button</MyButton>
  <MyButton variant="rounded" >My rounded Button</MyButton> -->
  <p></p>
</template>

<style lang="scss">
.recipes-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
  margin-bottom: 100px;
}
</style>
