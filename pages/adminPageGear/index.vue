<template>
  <div class="container">
    <h3 class="text-white mt-4">Administrator Gears</h3>
    <div class="d-grid gap-2">
      <nuxt-link to="/adminPageGear/form/TambahImage" class="btn btn-primary mt-2 mb-4">Set Image</nuxt-link>
    </div>
    <div class='row row-cols-1 mb-4 row-cols-md-1 g-4'>
        <GearItemAdmin
          v-for="(item, index) in items"
          :key="index"
          :title="item?.title"
          :img="item?.img"
          :main-des="item?.mainDes"
          :description="item?.description"
          :price="item?.price"
          :item-id="item?.id"
        />
    </div>
    <div class="d-grid gap-2">
      <nuxt-link to="/adminPageGear/form/TambahGear" class="btn btn-primary mb-2">Add Gear</nuxt-link>
    </div>
  </div>
</template>
<script>
import GearItemAdmin from "@/components/adminPage/GearAdmin/GearItemAdmin.vue"
export default {
  components: {
    GearItemAdmin
  },
  layout: 'admin',
  data () {
    return {
      items: []
    }
  },
  mounted() {
    this.getCards();
  },
  methods: {
    async getCards() {
      const response = await this.$axios.get("/rest/v1/items", {
        headers: {
          apikey: process.env.supabaseKey
        }
      })
      this.items = response?.data
    },
  },
}
</script>