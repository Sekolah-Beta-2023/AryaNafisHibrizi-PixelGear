<template>
  <div class="container my-2">
    <form @submit.prevent="onFormSubmit">
      <div class="form-group my-2">
        <label for="title" class="text-white">Judul Artikel</label>
        <input id="title" type="text" class="form-control" name="title">
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
        <label for="link" class="text-white">Link Web</label>
        <input id="link" type="text" class="form-control" name="link">
      </div>
      <div class="d-grid gap-2">
        <button class="btn btn-primary" type="submit">Tambah Article</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  layout: 'admin',
  data() {
    return{
      img: `${process.env.supabaseApi}/storage/v1/object/public/photoCard/`
    }
  },
  methods: {
    async onFormSubmit () {
      const dataForm = {
        title: document.getElementById("title").value,
        description: document.getElementById("description").value,
        img: document.getElementById("img").value,
        link: document.getElementById("link").value,
      }
      const response = await fetch(process.env.supabaseApi + '/rest/v1/cards', {
        method: 'POST',
        headers: {
          apikey: process.env.supabaseKey,
          "Content-Type": "application/json",
          Prefer: "return=representation"
        },
        body: JSON.stringify(dataForm)
      })
      const data = await response?.json()
      this.$router.push(`/adminPageCard/detail/${data[0]?.id}`)
      console.log(data)
    }
  }
}
</script>