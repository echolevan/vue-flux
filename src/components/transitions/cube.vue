<template>
	<flux-cube :slider="slider" :index="index" ref="cube"></flux-cube>
</template>

<script>
	import FluxCube from '../FluxCube.vue';

	export default {
		name: 'transitionCube',

		components: {
			FluxCube
		},

		data: () => ({
			currentImage: undefined,
			nextImage: undefined,
			index: {},
			totalDuration: 1000,
			perspective: '1600px',
			easing: 'ease-out'
		}),

		props: {
			slider: Object
		},

		computed: {
			cube: function() {
				return this.$refs.cube;
			}
		},

		created() {
			this.totalDuration = this.slider.config.duration || 1000;

			this.currentImage = this.slider.currentImage();
			this.nextImage = this.slider.nextImage();

			this.slider.setTransitionOptions(this);

			this.index = {
				front: this.currentImage.index,
				left: this.nextImage.index,
				right: this.nextImage.index
			};
		},

		mounted() {
			this.slider.mask.style.perspective = this.perspective;

			this.currentImage.hide();
			this.nextImage.hide();

			this.cube.setCss({
				transition: 'all '+ this.totalDuration +'ms '+ this.easing
			});

			this.cube.turn(this.direction);
		},

		destroyed() {
			this.slider.mask.style.perspective = 'none';

			this.nextImage.show();
		}
	};
</script>
