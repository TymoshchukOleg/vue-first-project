<template>
	<div>
		<div class="products" 
			v-for="product in products" 
			:key="product.id">
				{{ product.id }}
				{{ product.name }}
				{{ product.body }}
				{{ product.filters }}
				<button @click="addToCart(product.id)">+</button>
				<button @click="removeFromCart(product.id)">-</button>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		products: {
			type: Array,
			default: () => [],
		},
		cart: {
			type: Array,
			deafult: () => [],
		}
	},
	methods: {
		addToCart: function(id){
			this.$emit('addToCart', id-1);
		}, 
		removeFromCart: function(id){
			this.$emit('removeFromCart', id);
		},
	}
};
</script>

<style lang="css" scoped>
</style>
