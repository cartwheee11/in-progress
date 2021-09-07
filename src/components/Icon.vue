<template>
	<div>
		<div class="icon">
			<img :src="img" alt="">
		</div>
		<p>{{title}}</p>
	</div>
		

	
</template>

<script>
	export default {
		props: {
			title: {
				type: String,
				default: 'default title',
				reqired: true
			},

			img: {
				type: String,
				required: true,
			}
		},

		mounted() {

		}
	}
</script>

<style scoped>
	* {
		color:  white;
	}

	.icon {

	}
	
/*	.container {
		height: 100px;
	}*/

	p {
		display: inline-block;
	}
</style>