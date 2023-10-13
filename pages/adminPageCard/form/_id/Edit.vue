<template>
  <div class="container my-2">
    <form @submit.prevent="onFormSubmit">
      <input id="id" v-model="title" type="hidden" class="form-control" name="id">
      <div class="form-group my-2">
        <label for="title" class="text-white">Judul Artikel</label>
        <input v-model="title" id="title" type="text" class="form-control" name="title">
      </div>
      <div class="form-group my-2">
        <label for="description" class="text-white">Description</label>
        <textarea v-model="description" id="description" class="form-control" name="description" rows="3"></textarea>
      </div>
      <div class="form-group my-2">
        <label for="img" class="text-white">Link Image</label>
        <input v-model="img" id="img" type="text" class="form-control" name="img">
      </div>
      <div class="form-group my-2">
        <label for="link" class="text-white">Link Web</label>
        <input v-model="link" id="link" type="text" class="form-control" name="link">
      </div>
      <button class="btn btn-primary" type="submit">Finish</button>
    </form>
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
    async onFormSubmit() {
      const dataForm = {
        title: document.getElementById("title").value,
        description: document.getElementById("description").value,
        img: document.getElementById("img").value,
        link: document.getElementById("link").value,
      }
      const response = await fetch(process.env.supabaseApi + '/rest/v1/cards?id=eq.' + this.cardId, {
        method: 'PATCH',
        headers: {
          apikey: process.env.supabaseKey,
          "Content-Type": "application/json",
          Prefer: "return=representation"
        },
        body: JSON.stringify(dataForm)
      })
      const data = await response?.json()
      this.$router.push(`/adminPageCard/detail/${data[0]?.id}`)
    }
  }

}
</script>