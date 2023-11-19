<script setup>
import { ref } from "vue"
import MyPerson from "@/components/MyPerson.vue"

const list = ref(['Un', 'Deux', 'Trois', 'Quatre'])
const people = ref([
  { firstName: 'Homer', age: 55 },
  { firstName: 'Marge', age: 32 }
])
</script>

<template>
  <div class="demo-view">
    <ul>
      <li v-for="person in people">
        <MyPerson :name="person.firstName" :age="person.age" />
        <MyPerson v-bind="{ name: person.firstName, age: person.age }" />
        <MyPerson v-bind="person" />
      </li>
    </ul>
  </div>
</template>

<style lang="scss">

</style>
