<template>
  <div class="container mb-2">
    <div class="form-group mb-4">
      <form @submit.prevent="onFormSubmit" ref="imageForm" enctype="multipart/form-data">
        <label for="file" class="text-white my-2">Upload Image:</label>
        <br>
        <input id="file" name="file" ref="fileInput" type="file">
        <br>
        <button class="btn btn-primary mt-2" type="submit">Add Image</button>
      </form>
    </div>
    <div class="form-group mb-4">
      <form @submit.prevent="onFormDelete">
        <label for="img" class="text-white my-2">Delete Image:</label>
        <br>
        <input id="img" name="img" type="text">
        <br>
        <button class="btn btn-danger mt-2" type="submit">Delete Image</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'admin',
  data() {
    return {
    }
  },
  methods: {
    async onFormSubmit () {
      const input = this.$refs.fileInput;
      const dataForm = input.files[0].name
      const data = new FormData(this.$refs?.imageForm)
      await fetch(process.env.supabaseApi + '/storage/v1/object/photoCard/' + dataForm, {
        method: 'POST',
        headers: {
          'Authorization': 'Bearer ' + process.env.supabaseKey, 
        },
        body: data
      })
      location.reload();
    },
    onFormDelete () {
      const link = document.getElementById("img").value
      console.log(link)
      fetch(process.env.supabaseApi + '/storage/v1/object/photoCard/' + link, {
        method: 'DELETE',
        headers: {
          'Authorization': 'Bearer ' + process.env.supabaseKey, 
        }
      })
      location.reload();
    }
  }
}
</script>