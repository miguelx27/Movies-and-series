<template>
	<div class="list-item">
		<Item v-for="item in items" :image="item.Poster" :title="item.Title" :year="item.Year" />
	</div>

</template>

<script type="text/javascript">
import Item from './Item.vue';
export default {
	props: {
		items: {
			type: Array,
			default: [],
		},
	},

	components: {
		Item
	}
}
</script>

<style type="text/css">
.list-item {
	display: flex;
	flex-wrap: wrap;
}	
</style>