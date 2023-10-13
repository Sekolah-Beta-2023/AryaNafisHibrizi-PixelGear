<template>
	<div class="container">
    <h5 class="my-4 text-white">Select the Gear Setup You Want</h5>
    <div class="title border-bottom d-flex align-items-center pb-1 my-3">
      <div class="d-flex align-items-center justify-content-start w-50">
        <input v-model="filterQuery" type="text" class="form-control text-white bgSearch" placeholder="Search">
        <div class="dropdown ms-2">
          <select v-model="filterQuery" class="btn dropdown-toggle border text-white bgOrng">
            <option value="">All</option>
            <option value="Camera">Camera</option>
            <option value="Lighting">Lighting</option>
            <option value="Gimbal">Gimbal</option>
            <option value="Tripod">Tripod</option>
          </select>
        </div>
      </div>
      <div class="d-flex align-items-center justify-content-end w-50">
        <span class="me-2 text-white">View As</span>
          <button
            class="btn btn-outline-secondary py-1 px-3 border-white text-white bgOrng me-2"
            @click="isGrid = !isGrid"
          >
            {{ isGrid ? 'Grid' : 'List' }}
          </button>
          <button class="btn btn-outline-secondary py-1 px-3 border-white text-white bgOrng" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasWithBothOptions" aria-controls="offcanvasWithBothOptions">Cart</button>
      </div>
    </div>
    <div
      :class="[
        'row row-cols-1 mb-5',
        isGrid ? 'row-cols-md-4 g-4' : 'row-cols-md-1 g-4']"
    >
        <ItemGear
          v-for="(item, index) in resultQuery"
          :key="index"
          :item="item"
          :is-grid="isGrid"
          :index="index"
          @handleButtonClick="handleButtonClick"
        />
    </div>
    <div id="offcanvasWithBothOptions" class="offcanvas offcanvas-start text-bg-dark" data-bs-scroll="true" tabindex="-1" aria-labelledby="offcanvasWithBothOptionsLabel">
      <div class="offcanvas-header bgOrng p-2">
        <h5 id="offcanvasWithBothOptionsLabel" class="offcanvas-title"><strong>List You Cart</strong></h5>
        <button type="button" class="btn-close btn-close-white" data-bs-dismiss="offcanvas" aria-label="Close"></button>
      </div>
      <div class="offcanvas-body p-0">
        <OffCanvas
          v-for="(isiCart, index) in isiCarts"
          :key="index"
          :isi-cart="isiCart"
          :index="index"
          @incrementCounter="incrementCounter"
          @decrementCounter="decrementCounter"
          @resetItemCart="resetItemCart"
          />
      </div>
      <div class="bgOrng d-flex justify-content-start">
        <h6 class="m-2">Price Total: Rp<strong>{{total}}</strong> for <strong>{{daysBorrow}} Day</strong></h6>
        <button type="button" class="button btn btn btn-dark btn-sm p-0 ms-2 my-auto" @click="incrementDay">+</button>
        <button type="button" class="button btn btn btn-dark btn-sm p-0 ms-1 my-auto" @click="decrementDay">-</button>
      </div>
      <div class="d-grid gap-2">
        <button class="btn btn-checkout text-white" type="button"><strong>Checkout</strong></button>
      </div>
    </div>
    <ul v-for='(cart, index) in isiCarts' :key="index">
      <li>{{cart}}</li>
    </ul>
	</div>
</template>
<script>
import ItemGear from "@/components/Item/ItemGear.vue"
import OffCanvas from "@/components/OffCanvas/OffCanvas.vue"
export default {
    components: {
    ItemGear,
    OffCanvas
  },
  data() {
    return {
      // Daftar task
      items: [],
      // Tipe layout daftar task
      isGrid: false,
      // Variabel penampung teks pencarian
      filterQuery: '',
      // Penampung cart
      isiCarts: [],
      // Penampung keterangan lama meminjam
      daysBorrow: 1
    }
  },
  computed: {
    resultQuery() {
      if (this.filterQuery) {
        return this.items.filter((gear) => {
          return this.filterQuery
            .toLowerCase()
            .split(" ")
            .every((v) => gear.title.toLowerCase().includes(v));
        });
    }
      else {
        return this.items
      }
    },
    total() {
      const total = this.isiCarts.reduce((total, item) => total + (item.price * item.amount), 0); 
      return total * this.daysBorrow
    },
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
    handleButtonClick(dataIndex) {
      for (let i = 0; i < this.isiCarts.length; i++) {
        if (this.isiCarts[i].title === this.items[dataIndex].title) {
          return this.isiCarts[i].amount++
        }
      }
      this.isiCarts.push(this.items[dataIndex])
    },
    incrementCounter(dataIndex) {
      this.isiCarts[dataIndex].amount++
    },
    decrementCounter(dataIndex) {
      if (this.isiCarts[dataIndex].amount === 1) {
        return alert('The Minimum Amount Of Item Must Be 1')
      }
      this.isiCarts[dataIndex].amount--
    },
    resetItemCart(dataIndex) {
      this.isiCarts.splice([dataIndex], 1)
    },
    incrementDay() {
      this.daysBorrow++
    },
    decrementDay() {
      if (this.daysBorrow === 1) {
        return alert('The Minimum Amount day to borrow is 1 day')
      }
      this.daysBorrow--
    }
  }
}
</script>
<style scoped>
  .bgOrng{
    background-color: rgb(206, 102, 5);
  }
  .bgSearch{
    background-image: linear-gradient(to right, rgb(0, 0, 0)20%, rgba(206, 102, 5));
  }
  input::placeholder {
  color: white;
  }
  .button{
    width: 45px;
    height: 25px;
    color: rgba(206, 102, 5);
  }
  .btn-checkout{
    background-color: #00C87C;
  }
</style>
