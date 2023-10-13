<template>
  <div class="card border-secondary">
    <img :src="card.img" class="card-img-top image" alt="err">
    <div class="card-body text-white">
      <h5 class="card-title">{{card.title}}</h5>
      <p class="card-text">{{card.description}}</p>
      <a :href="card.link" class="stretched-link text-warning" target="_blank">Continue Learning</a>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    card: {
      type: Object,
      default: () => {}
    }
  }
}
</script>
<style scoped>
  .card-body{
    background-color:rgb(50, 50, 50);
  }
</style>