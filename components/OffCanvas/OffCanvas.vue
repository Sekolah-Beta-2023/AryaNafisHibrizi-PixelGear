<template>
	<div class="border border-secondary p-1">
		<strong class="ms-2">{{isiCart.title}}</strong>
		<div class="d-flex flex-row">
			<img :src="isiCart.img" alt="err" class="ms-2 mb-2 mt-1">
			<div class="d-flex flex-column ms-2">
        <strong>Rp{{isiCart.price}} /Day</strong>
        <p class="mb-1"><strong>Amount:</strong> {{isiCart.amount}}</p>
        <button type="button" class="btn btn btn-light btn-sm mb-1 p-0" @click="incrementCounter">+</button>
        <button type="button" class="btn btn btn-light btn-sm p-0" @click="decrementCounter">-</button>
		</div>
        <div class="d-flex flex-column ms-2">
        <button type="button" class="btn-close btn-close-white ms-5" @click="resetItemCart"></button>
		</div>
		</div>
	</div>
</template>
<script>
export default {
	props: {
		isiCart: {
			required: true,
			type: Object
		},
    index: {
      type: Number,
      required: true
    }
	},
  methods: {
    incrementCounter() {
      this.$emit('incrementCounter', this.index)
    },
    decrementCounter() {
      this.$emit('decrementCounter', this.index)
    },
    resetItemCart() {
      this.$emit('resetItemCart', this.index)
    },
  }
}
</script>
<style scoped>
	img{
		width: 165px;
	}
  .btn{
    width: 60px;
    height: 25px;
    color: rgba(206, 102, 5);
  }
</style>