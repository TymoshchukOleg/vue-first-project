<template>
	<div>
		<div 
			v-for="filter in filters" 
			:key="filter.id" 
			@click='myFilter(filter.id)'
			>
				<!-- <div v-if="activeFilters.includes(filter.id)" class="active">
					{{ filter.id }}
					{{ filter.title }}
				</div>
				<div v-else class="filter">
					{{ filter.id }}
					{{ filter.title }}
				</div> -->
				<div class="filter" :class="[{active: activeFilters.includes(filter.id)}]">
					{{ filter.id }}
					{{ filter.title }}
				</div>
		</div>
		<button class="clear-button" @click='clearAllFilters(activeFilters)'>Clear</button>
	</div>
</template>

<script>
export default {
	data() {
		return {
			activeFilters: [],
		}
	},
	props: {
		filters: {
			type: Array,
			default: () => [],
		},
	},
	methods: {
		myFilter(id) {
			if(!this.activeFilters.includes(id)) {
				this.activeFilters.push(id);
			} else {
				this.activeFilters.forEach((item, index, array) => {
					if(item === id) {
						array.splice(index, 1);
					}
				})
			}
			this.$emit('changeFilter', id, this.activeFilters);
		},
		clearAllFilters: function(activeFilters) {
			activeFilters.length = 0;
		},
	},
};
</script>

<style>
.filter.active {
	color: red;
	border: 2px solid red;
}

.clear-button {
	padding: 10px;
	margin-top: 5px;
	background: #fff;
	border: 2px solid black;
	cursor: pointer;
}
.filter {
	border: 2px solid black;
	color: black;
	padding: 10px;
	margin: 5px;
	cursor: pointer;
}
</style>
