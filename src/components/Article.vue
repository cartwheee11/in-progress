<template>
		<!-- <template v-slot="innerHtml"></template> -->
		<div class="content" v-html="innerHtml"></div>
</template>

<script>
	let axios = require('axios');

	export default {
		props: {
			path: {
				type: String,
				required: false,
				default: '/home/articles/first.html'
			}
		},

		data() {
			return {
				innerHtml: '<p>loading...</p>'
			}
		}, 

		methods: {
			onRef(ref) {
				this.$emit("lolref", ref);
			}
		},

		async mounted () {
			let res = await axios(this.path)
			this.innerHtml = await res.data;
		}
		
	}
</script>

<style scoped>
	.content {
		display: block;
		padding: 20px;
	}

	
</style>

