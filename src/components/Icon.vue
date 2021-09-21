<template>
	<div>
		<div class="icon">
			<img :src="img" alt="">
		</div>
		<p class="p">{{title}}</p>
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

	.p {
		display: inline-block;
		color: black;
		background: white;
		padding: 0 6px;
		margin-top: 0;
		/* border-radius: 4px; */
		text-transform: uppercase;
		/* display: block; */
		color: #000;
		background: #fff;
		position: relative;
		/* width: 300px; */
		/* padding: 20px; */
		margin: 10px auto;
		border-top: 2px solid white;
		border-bottom: 2px solid white
	}

	.p:before,
	.p:after {
		content: '';
		top: 0;
		width: 2px;
		height: 100%;
		position: absolute;
		background: white;
	}
	.p:before {
		left: -2px;
	}
	.p:after {
		right: -2px;
	}

	img {
		image-rendering: optimizeSpeed;             /*                     */
    image-rendering: -moz-crisp-edges;          /* Firefox             */
    image-rendering: -o-crisp-edges;            /* Opera               */
    image-rendering: -webkit-optimize-contrast; /* Chrome (and Safari) */
    image-rendering: pixelated;                 /* Chrome as of 2019   */
    image-rendering: optimize-contrast;         /* CSS3 Proposed       */
    -ms-interpolation-mode: nearest-neighbor;   /* IE8+                */
	}
</style>