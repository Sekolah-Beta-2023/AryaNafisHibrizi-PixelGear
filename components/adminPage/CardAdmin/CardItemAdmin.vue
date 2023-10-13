<template>
  <div class="p-3">
    <div class="card" style="width: 250px;">
      <img :src="img" class="card-img-top" alt="err">
      <div class="card-body">
        <h5 class="card-title text-white">{{title}}</h5>
        <p class="card-text text-truncate text-white">{{description}}</p>
        <a :href="link" class="text-warning" target="_blank">Continue Learning</a>
        <br>
        <nuxt-link :to="`/adminPageCard/detail/${cardId}`" class="btn btn-primary mt-2">Edit This</nuxt-link>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    title: {
      type: String,
      default: ""
    },
    description: {
      type: String,
      default: ""
    },
    cardId: {
      type: String,
      default: ""
    },
    img: {
      type: String,
      default: ""
    },
    link: {
      type: String,
      default: ""
    }
  }
}
</script>
<style scoped>
  .card-body{
    background-color:rgb(50, 50, 50);
  }
</style>