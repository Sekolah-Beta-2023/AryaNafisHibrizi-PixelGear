<template>
  <div class="container my-2">
    <form @submit.prevent="onFormSubmit">
      <input id="id" v-model="title" type="hidden" class="form-control" name="id">
      <div class="form-group my-2">
        <label for="title" class="text-white">Product Name</label>
        <input v-model="title" id="title" type="text" class="form-control" name="title">
      </div>
      <div class="form-group my-2">
        <label for="mainDes" class="text-white">mainDes</label>
        <textarea v-model="mainDes" id="mainDes" class="form-control" name="mainDes" rows="3"></textarea>
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
        <label for="amount" class="text-white">Amount / Product</label>
        <input v-model="amount" id="amount" type="text" class="form-control" name="amount">
      </div>
      <div class="form-group my-2">
        <label for="price" class="text-white">Price</label>
        <input v-model="price" id="price" type="text" class="form-control" name="price">
      </div>
      <div class="d-grid gap-2">
        <button class="btn btn-primary" type="submit">Finish</button>
      </div>
    </form>
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
      this.mainDes = data[0]?.mainDes
      this.description = data[0]?.description
      this.img = data[0]?.img
      this.amount = data[0]?.amount
      this.price = data[0]?.price
      this.itemId = data[0]?.id
    },
    async onFormSubmit() {
      const dataForm = {
        title: document.getElementById("title").value,
        mainDes: document.getElementById("mainDes").value,
        description: document.getElementById("description").value,
        img: document.getElementById("img").value,
        amount: document.getElementById("amount").value,
        price: document.getElementById("price").value,
      }
      const response = await fetch(process.env.supabaseApi + '/rest/v1/items?id=eq.' + this.itemId, {
        method: 'PATCH',
        headers: {
          apikey: process.env.supabaseKey,
          "Content-Type": "application/json",
          Prefer: "return=representation"
        },
        body: JSON.stringify(dataForm)
      })
      const data = await response?.json()
      this.$router.push(`/adminPageGear/detail/${data[0]?.id}`)
    }
  }

}
</script>