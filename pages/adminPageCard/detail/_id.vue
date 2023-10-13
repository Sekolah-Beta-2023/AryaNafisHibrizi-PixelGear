<template>
  <div class="container py-4" style="width: 600px;">
    <div class="card 0">
      <button class="btn btn-primary mx-4 my-2" to="/adminPageCard/form/TambahCard" @click="onEdit">Edit Artikel</button>
      <div class="card-body">
        <h5 class="card-title">{{ title }}</h5>
        <p class="card-text">{{ description }}</p>
        <p class="card-text">{{ link }}</p>
      <img :src="img" class="card-img-top image" alt="err">
        <p class="card-text">{{ img }}</p>
      </div>
      <button class="btn btn-primary mx-4 mb-4" to="/adminPageCard" @click="onEnd">Selesai</button>
      <button type="button" class="btn btn-danger" @click="deleteCard">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'admin',
  data() {
    return {
      title: '',
      description: '',
      img: '',
      link: '',
      cardId: ''
    }
  },
  mounted() {
    const params = this.$route.params
    this.getDetailData(params?.id)
  },
  methods: {
    async getDetailData (cardId) {
      const response = await fetch(process.env.supabaseApi + '/rest/v1/cards?id=eq.' + cardId, {
        headers: {
          apikey: process.env.supabaseKey
        }
      })

      const data = await response.json()

      this.title = data[0]?.title
      this.description = data[0]?.description
      this.img = data[0]?.img
      this.link = data[0]?.link
      this.cardId = data[0]?.id
    },
    onEdit() {
      this.$router.push(`/adminPageCard/form/${this.cardId}/edit`)
    },
    onEnd() {
      this.$router.push(`/adminPageCard`)
    },
    deleteCard() {
      this.deleteCards()
    },
    async deleteCards() {
      const response = await this.$axios.delete("/rest/v1/cards?id=eq." + this.cardId, {
        headers: {
          apikey: process.env.supabaseKey
        }
      })
      this.cards = response?.data
      this.$router.push(`/adminPageCard`)
    }
  }
}
</script>
