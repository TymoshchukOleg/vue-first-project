<template>
    <div class="product" v-for="item in cart" :key="item.id">
        {{ item.id }}
        {{ item.name }}
		{{ item.body }}
		{{ item.filters }}
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
}
</script>

<style scoped>
.product {
    padding: 10px;
    border: 2px solid black;
    cursor: pointer;
    margin: 5px;
}
</style>