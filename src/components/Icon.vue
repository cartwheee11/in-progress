<template>
	<div class="icon-container">
		<div class="icon" :style="'background-image: url(' + img + ')'" :class="type + '-icon'">
			<!-- <img :src="img" alt="" :class="type + '-icon'" > -->
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

			type: {
				type: String,
				required: false
			},

			img: {
				type: String,
				required: true,
			}
		},

		data() {
			return {
				imageIconStyles: {
					// border: '5px white solid',
					'background-size': '100px'
				}
			}
		},
	}
</script>

<style scoped>
	* {
		color:  white;
		/* width: 100px; */
	

	}

	.icon-container {
		transition: transform 0.1s;
		/* width: 100%; */
		/* height: 100%; */
		padding-top: 10px;

	}

	.icon {
		/* width: 100%; */
		width: 80px;
		height: 70px;
		margin: 0 auto;
		/* margin: 0 !important; */
		/* height: 100%; */
		/* background-size: contain; */
		background-position: center;
		background-repeat: no-repeat;

		image-rendering: optimizeSpeed;                                
    image-rendering: -moz-crisp-edges;        
    image-rendering: -o-crisp-edges;            
    image-rendering: -webkit-optimize-contrast; 
    image-rendering: pixelated;                 
    image-rendering: optimize-contrast;         
    -ms-interpolation-mode: nearest-neighbor;   
		/* max-width: 80px; */
		/* max-height: 80px; */
	}

	.icon-container:hover{
		/* box-shadow: 3px 3px 6px 1px rgba(255, 255, 255, 0.7); */
		/* border-radius: 10px; */
		/* filter: drop-shadow(0px 0px 3px white); */
		transform: translate(0, -5px);
		transition: transform 0.1s;
	}

	/* .icon:hover {
		background: white
	} */
	
/*	.container {
		height: 100px;
	}*/

	.image-icon {
		border: 3px solid white;
		background-size: cover;
		height: 100px;
		/* display: block; */
		/* width: 100%; */
		/* height: 100%; */
		/* width: 100px; */
		/* height: 100px; */
	}

	/* .image-icon:before,
	.image-icon:after {
		content: ' ';
		top: 0;
		width: 2px;
		height: 100%;
		position: absolute;
		background: white;
		
	} */
	.image-icon:before {
		left: -2px;
	}
	.image-icon:after {
		right: -2px;
	}

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
		image-rendering: optimizeSpeed;                                
    image-rendering: -moz-crisp-edges;        
    image-rendering: -o-crisp-edges;            
    image-rendering: -webkit-optimize-contrast; 
    image-rendering: pixelated;                 
    image-rendering: optimize-contrast;         
    -ms-interpolation-mode: nearest-neighbor;   
		max-width: 80px;
		max-height: 80px;
	}
</style>