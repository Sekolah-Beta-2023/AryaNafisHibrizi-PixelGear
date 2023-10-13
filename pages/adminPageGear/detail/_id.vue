<template>
  <div class="container py-4" style="width: 600px;">
    <div class="card 0">
      <button class="btn btn-primary mx-4 my-2" to="/adminPageGear/form/TambahGear" @click="onEdit">Edit Item Gear</button>
      <div class="card-body">
        <h5 class="card-title">{{ title }}</h5>
        <p class="card-text">{{ mainDes }}</p>
        <p class="card-text">{{ description }}</p>
      <img :src="img" class="card-img-top image" alt="err">
        <p class="card-text">{{ img }}</p>
        <p class="card-text">{{ amount }}</p>
        <p class="card-text">{{ price }}</p>
      </div>
      <button class="btn btn-primary mx-4 mb-4" to="/adminPageGear" @click="onEnd">Finish</button>
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
      mainDes: '',
      description: '',
      img: '',
      amount: '',
      price: '',
      itemId: ''
    }
  },
  mounted() {
    const params = this.$route.params
    this.getDetailData(params?.id)
  },
  methods: {
    async getDetailData (itemId) {
      const response = await fetch(process.env.supabaseApi + '/rest/v1/items?id=eq.' + itemId, {
        headers: {
          apikey: process.env.supabaseKey
        }
      })

      const data = await response.json()

      this.title = data[0]?.title
      this.description = data[0]?.description
      this.img = data[0]?.img
      this.link = data[0]?.link
      this.itemId = data[0]?.id
    },
    onEdit() {
      this.$router.push(`/adminPageGear/form/${this.itemId}/edit`)
    },
    onEnd() {
      this.$router.push(`/adminPageGear`)
    },
    deleteCard() {
      this.deleteCards()
    },
    async deleteCards() {
      const response = await this.$axios.delete("/rest/v1/items?id=eq." + this.itemId, {
        headers: {
          apikey: process.env.supabaseKey
        }
      })
      this.cards = response?.data
      this.$router.push(`/adminPageGear`)
    }
  }
}
</script>
