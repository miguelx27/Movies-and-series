<template>
	<div class="item" :style="`background-image: url(${image});`">
		<div class="item__description">
			<p>{{ title }}</p>
			<p>{{ year }}</p>
		</div>
	</div>
</template>

<script type="text/javascript">
	export default {
		props: {
			image: {
				type: String,
				default: '',
			},

			title: {
				type: String,
				default: '',
			},

			year: {
				type: String,
				default: '',
			}
		},
	}
</script>

<style lang="scss">
.item{
height: 350px;
width: 250px;
margin: 5px;
display: flex;

&__description {
	text-align: center;
	flex: 1;
	align-self: flex-end;
	color: white;
	background-color: rgba(black, .5);
	padding-top: 10px;
}
}

</style>