<template>
  <section class="memory-game">
    <nav><button @click="reset" class="reset-button">Reset</button></nav>
    <div v-for="(card, i) in memoryCards" :key="i" @click='flipCard(card)' class="memory-card" v-bind:class="{'flip': card.isFlipped, 'matched': card.isMatched}">
      <img :src="require(`@/assets/img/${card.icon}.svg`)" alt="" class="front-face">
      <img src="@/assets/img/js-badge.svg" alt="" class="back-face">
    </div>
  </section>
</template>

<script>
import cards from '@/cards.json'
import _ from 'lodash'

export default {
  data () {
    return {
      memoryCards: cards,
      flippedCards: [],
      finish: false,
      difficulty: 'normal'
    }
  },
  created () {
    this.memoryCards = this.memoryCards.concat(_.cloneDeep(this.memoryCards))
    this.reset()
  },
  computed () {
  },
  methods: {

    flipCard (card) {
      if (card.isMatched || card.isFlipped || this.flippedCards.length === 2) return

      card.isFlipped = !card.isFlipped

      if (this.flippedCards.length < 2) {
        this.flippedCards.push(card)
      }
      if (this.flippedCards.length === 2) {
        this.matchCards(card)
      }
    },

    matchCards (card) {
      if (this.flippedCards[0].icon === this.flippedCards[1].icon) {
        setTimeout(() => {
          // eslint-disable-next-line no-return-assign
          this.flippedCards.forEach(card => card.isMatched = true)
          this.flippedCards = []

          if (this.memoryCards.every(card => card.isMatched === true)) {
            this.finish = true
          }
        }, 400)
      } else {
        setTimeout(() => {
        // eslint-disable-next-line no-return-assign
          this.flippedCards.forEach(card => card.isFlipped = false)
          this.flippedCards = []
        }, 800)
      }
    },

    reset () {
      console.log('clicked')
      this.memoryCards.forEach((card) => {
        card.isFlipped = false
        card.isMatched = false
      })

      setTimeout(() => {
        if (this.difficulty === 'easy') {
          this.memoryCards = this.memoryCards.sort((a, b) => (a.icon > b.icon) ? 1 : ((b.icon > a.icon) ? -1 : 0)).slice(0, 8)
        }
        this.memoryCards = _.shuffle(this.memoryCards)
        this.finish = false
        this.flippedCards = []
      }, 400)
    }

  }
}
</script>
