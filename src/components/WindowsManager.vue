<template>
	
	<Article/>

</template>

<script>
	import Article from './Article.vue';

	export default {
		components: {
			Article
		},

		props: {
			windows: {
				type: Array,
				required: false,
				default: new Array(
					{
						type: 'article',
						url: 'home/articles/first.html'
					},
					{
						type: 'article',
						url: 'home/articles/second.html'
					},
					{
						type: 'window',
						content: '<p>hrllo</p>'
					}
				)
			}
		},

	


	}

</script>

<style>
	

</style>