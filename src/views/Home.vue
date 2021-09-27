<template>
  <section class="memory-game">
    <Item
      v-for="product in memoryCards"
      :key="product.id"
      :product="product"
      @card-has-flipped="cardFlipped"
      :hasFlippedCard="hasFlippedCard"
      :firstCard="firstCard"
      @update-first-card="updateFirstCard"
      :secondCard="secondCard"
      @update-second-card="updateSecondCard"
    />
  </section>
</template>

<script>
import Item from '@/components/Item.vue'

export default {
  data () {
    return {
      hasFlippedCard: false,
      firstCard: null,
      secondCard: null
    }
  },
  props: ['memoryCards'],
  components: {
    Item
  },
  methods: {
    cardFlipped () {
      this.hasFlippedCard = !this.hasFlippedCard
    },
    updateFirstCard (card) {
      this.firstCard = card
    },
    updateSecondCard (card) {
      this.secondCard = card
    }
  }
}
</script>
