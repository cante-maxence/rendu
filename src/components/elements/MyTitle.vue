<script setup>
import { computed } from 'vue'

const props = defineProps({
  el: String,
  size: String
})

const className = computed(() => ({
  'title' : true,
  '-l': props.size === 'large',
  '-m': props.size === 'medium',
  '-xl': props.size === 'xlarge',
  '-s': props.size === 'small'
}))
</script>
<template>
  <h4 v-if="el === 'h4'" :class="className">
    <slot></slot>
  </h4>
  <h3 v-else-if="el === 'h3'" :class="className">
    <slot></slot>
  </h3>
  <h2 v-else-if="el === 'h2'" :class="className">
    <slot></slot>
  </h2>
  <h1 v-else :class="className">
    <slot></slot>
  </h1>
</template>

<style lang="scss">
.title {
  font-family: $primary-font-family;
  font-size: rem(18);
  font-weight: 700;
  word-wrap: break-word;
  > span{
    color: $primary-color;
  }
  &.-xl {
    font-size: rem(48);
  }
  &.-l{
    font-size: rem(24);
  }
  &.-m{
    font-size: rem(13);
  }
  &.-s {
    font-size: rem(9);
  }
}
@include x-large-up{
  .title {
    font-size: rem(36);
    &.-xl {
      font-size: rem(95);
    }
    &.-l{
      font-size: rem(48);
    }
    &.-m{
      font-size: rem(28);
    }
    &.-s {
      font-size: rem(18);
    }
  }
}
</style>
