<template>
	<flux-grid :slider="slider" :num-rows="numRows" :num-cols="numCols" :index="index" ref="grid"></flux-grid>
</template>

<script>
	import FluxGrid from '../FluxGrid.vue';

	export default {
		name: 'transitionBlinds2d',

		components: {
			FluxGrid
		},

		data: () => ({
			currentImage: undefined,
			nextImage: undefined,
			index: {},
			numRows: 1,
			numCols: 0,
			tileDuration: 1000,
			totalDuration: 0,
			easing: 'linear',
			tileDelay: 100
		}),

		props: {
			slider: Object
		},

		computed: {
			grid: function() {
				return this.$refs.grid;
			}
		},

		created() {
			this.tileDuration = this.slider.config.duration || 1000;
			this.tileDelay = Math.floor(this.tileDuration * 100 / 800);

			this.currentImage = this.slider.currentImage();
			this.nextImage = this.slider.nextImage();

			let divider = this.slider.size.width / 10;

			this.slider.setTransitionOptions(this, {
				numCols: Math.floor(this.slider.size.width / divider)
			});

			this.totalDuration = this.tileDelay * this.numCols + this.tileDuration;

			this.index = {
				front: this.currentImage.index
			};
		},

		mounted() {
			this.currentImage.hide();

			this.grid.transform((tile, i) => {
				tile.transform({
					transition: 'all '+ this.tileDuration +'ms '+ this.easing +' '+ this.getDelay(i) +'ms',
					opacity: '0.1',
					transform: 'scaleX(0)'
				});
			});
		},

		methods: {
			getDelay(i) {
				let delay = i;

				// if (this.direction === 'left')
				// 	delay = this.numCols - i - 1;

				return delay * this.tileDelay;
			}
		}
	};
</script>
