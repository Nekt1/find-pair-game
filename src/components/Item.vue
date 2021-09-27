<template>
    <div @click='flipCard' :data-framework="`${product.icon}`" class="memory-card" v-bind:class="{flip: isFlipped}">
      <img :src="require(`@/assets/img/${product.icon}.svg`)" alt="" class="front-face">
      <img src="@/assets/img/js-badge.svg" alt="" class="back-face">
    </div>
</template>

<script>
export default {
  data () {
    return {
      isFlipped: false
    }
  },
  props: ['product', 'hasFlippedCard', 'firstCard', 'secondCard'],
  methods: {
    flipCard () {
      this.isFlipped = !this.isFlipped

      if (!this.hasFlippedCard) {
        // first click
        this.$emit('card-has-flipped')
        this.$emit('updateFirstCard', this.product.icon)
      } else {
        // second click
        this.$emit('card-has-flipped')
        this.$emit('updateSecondCard', this.product.icon)
      }
    }
  }
}
</script>
