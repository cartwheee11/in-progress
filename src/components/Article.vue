<template>
	<window>
		<!-- <template v-slot="innerHtml"></template> -->
		<div class="content" v-html="innerHtml"></div>
	</window>
</template>

<script>
	import Window from './Window'
	let axios = require('axios')
	// let fetch = require('node-fetch')

	export default {
		components: {
			Window
		},

		props: {
			path: {
				type: String,
				required: false,
				default: './home/articles/first.html'
			}
		},

		data() {
			return {
				innerHtml: '<p>loading...</p>'
			}
		}, 

		async mounted () {
			let res = await axios(this.path)
			this.innerHtml = await res.data;
		}
		
	}
</script>

<style>


	.content {
		display: block;
		height: 100%;
		/*border:  1px red solid;*/
		/*position: absolute;*/
		/*width: 100%;*/
	}
</style>