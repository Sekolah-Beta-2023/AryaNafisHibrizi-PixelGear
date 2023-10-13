<template>
  <div>
    <HeaderAdmin />
    <Nuxt />
  </div>
</template>

<script>
import HeaderAdmin from '~/components/adminPage/HeaderAdmin.vue'
export default {
  components: {
    HeaderAdmin,
  }
}
</script>