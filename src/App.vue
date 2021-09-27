<template>
  <!-- <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div> -->
  <router-view/>
</template>

<script>
import cards from '@/cards.json'

export default {
  data () {
    return {
      memoryCards: cards,
      isActive: false
    }
  }
}
</script>
