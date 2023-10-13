<template>
  <div class="container my-2">
    <form @submit.prevent="onFormSubmit">
      <div class="form-group my-2">
        <label for="title" class="text-white">Product Name</label>
        <input id="title" type="text" class="form-control" name="title">
      </div>
      <div class="form-group my-2">
        <label for="mainDes" class="text-white">mainDes</label>
        <textarea id="mainDes" class="form-control" name="mainDes" rows="3"></textarea>
      </div>
      <div class="form-group my-2">
        <label for="description" class="text-white">Description</label>
        <textarea id="description" class="form-control" name="description" rows="3"></textarea>
      </div>
      <div class="form-group my-2">
        <label for="img" class="text-white">Link Image</label>
        <input id="img" v-model="img" type="text" class="form-control" name="img">
      </div>
      <div class="form-group my-2">
        <label for="amount" class="text-white">Amount / Product</label>
        <input id="amount" type="text" class="form-control" name="amount">
      </div>
      <div class="form-group my-2">
        <label for="price" class="text-white">Price</label>
        <input id="price" type="text" class="form-control" name="price">
      </div>
      <div class="d-grid gap-2">
        <button class="btn btn-primary" type="submit">Add Item Gear</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  layout: 'admin',
  data() {
    return{
      img: `${process.env.supabaseApi}/storage/v1/object/public/photoItems/`
    }
  },
  methods: {
    async onFormSubmit () {
      const dataForm = {
        title: document.getElementById("title").value,
        mainDes: document.getElementById("mainDes").value,
        description: document.getElementById("description").value,
        img: document.getElementById("img").value,
        amount: document.getElementById("amount").value,
        price: document.getElementById("price").value,
      }
      const response = await fetch(process.env.supabaseApi + '/rest/v1/items', {
        method: 'POST',
        headers: {
          apikey: process.env.supabaseKey,
          "Content-Type": "application/json",
          Prefer: "return=representation"
        },
        body: JSON.stringify(dataForm)
      })
      const data = await response?.json()
      this.$router.push(`/adminPageGear/detail/${data[0]?.id}`)
      console.log(data)
    }
  }
}
</script>