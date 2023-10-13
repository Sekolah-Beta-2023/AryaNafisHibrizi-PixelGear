<template>
  <div class="container">
    <h3 class="text-white mt-4">Administrator Cards</h3>
    <div class="d-grid gap-2">
      <nuxt-link to="/adminPageCard/form/TambahImage" class="btn btn-primary mt-2">Set Image</nuxt-link>
    </div>
    <div class="row row-cols-1 mb-3 row-cols-md-4 g-4">
      <CardItemAdmin
          v-for="(card, idx) in cards"
          :key="idx"
          :title="card?.title"
          :description="card?.description"
          :card-id="card?.id"
          :img="card?.img"
          :link="card?.link"
        />
    </div>
    <div class="d-grid gap-2">
      <nuxt-link to="/adminPageCard/form/TambahCard" class="btn btn-primary mb-2">Add Card</nuxt-link>
    </div>
  </div>
</template>
<script>
import CardItemAdmin from "@/components/adminPage/CardAdmin/CardItemAdmin.vue"
export default {
  components: {
    CardItemAdmin
  },
  layout: 'admin',
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
    },
  }
</script>
