<template>
  <div class="col">
    <div
      :class="[
        'card border-secondary',
        isGrid ? 'p-1' : 'kartu'
      ]"
    >
      <div
        :class="[
        '',
        isGrid ? '' : 'img'
        ]"
      >
      <img :src="item.img" class="card-img-top" alt="err">
      </div>
      <div
        :class="[
          'card-body',
          isGrid ? '' : 'kartu-bodi'
        ]"
      >
        <div
          :class="[
            'text-white',
            isGrid ? '' : 'text-section'
          ]"
        >
          <h5 class="card-title">{{item.title}}</h5>
          <p class="card-text" >{{item.mainDes}}.</p>
          <p v-if="!isGrid" class="card-text">{{item.description}}</p>
        </div>
        <div
          :class="[
            '',
            isGrid ? '' : 'cta-section'
          ]"
        >
          <div class="mt-2 text-white">Rp<strong>{{item.price}}</strong> / Day</div>
            <button type="button" class="btn btn-light mt-1" @click="triggerAddCart">Add to Cart</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    item: {
      type: Object,
      default: () => {
        return {}
      }
    },
    isGrid: {
      type: Boolean,
      required: true,
      default: false
    },
    index: {
      type: Number,
      required: true
    }
  },
  methods: {
    triggerAddCart() {
      this.$emit('handleButtonClick', this.index)
    }
  }
}
</script>
<style scoped>
  .card{
    background-color:rgb(50, 50, 50);
  }
  .kartu {
    flex-direction: row;
    max-width: 70em;
    box-shadow: 0 7px 7px rgba(0, 0, 0, 0.18);
  }
  .img {
    max-width: 20%;
    margin: auto;
    padding: 0.5em;
    border-radius: 0.7em;
  }
  .kartu-bodi {
    display: flex;
    justify-content: space-between;
  }
  .card-text {
    font-size: 0.9em;
    margin-bottom: 0;
  }
  .text-section {
    max-width: 60%;
  }
  .cta-section {
    max-width: 40%;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    justify-content: space-between;
  }
  .cta section .btn {
    padding: 0.3em 0.5em;
    background-color: #898989;
    border-color: #898989;
  }
</style>