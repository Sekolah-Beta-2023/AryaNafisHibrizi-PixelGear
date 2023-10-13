<template>
  <div class="container">
    <h3 class="mb-4 mt-3 text-white">Welcome To My Rentals "PixelGear"</h3>
    <h5 class="my-2 text-warning">Basics Of Photography That You Must Know:</h5>
    <div class="card-group">
      <CardItem
          v-for="(card, i) in cards"
          :key="i"
          :card="card"
        />
    </div>
    <br>
    <div class="d-grid gap-2 mb-5">
      <NuxtLink class="btn text-white" style="background-color: #00C87C;" aria-current="page" to="/gear">Let's Take a Actions!</NuxtLink>
    </div>
  </div>
</template>
<script>
import CardItem from "@/components/Card/CardItem.vue"
export default {
  components: {
    CardItem
  },
  data() {
    return {
      // Daftar task
      cards: []
    }
  },
  mounted() {
      this.getCards();
    },
    methods: {
      async getCards() {
        const response = await this.$axios.get("/rest/v1/cards", {
          headers: {
            apikey: process.env.supabaseKey
          }
        })
        this.cards = response?.data
      },
    }
  }
</script>