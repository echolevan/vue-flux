<template></template>

<script>
	export default {
		name: 'transitionFade',

		data: () => ({
			currentImage: undefined,
			nextImage: undefined,
			totalDuration: 1000,
			easing: 'ease-in'
		}),

		props: {
			slider: Object
		},

		created() {
          this.totalDuration = this.slider.config.duration || 1000;

          this.currentImage = this.slider.currentImage();
			this.nextImage = this.slider.nextImage();

			this.slider.setTransitionOptions(this);
		},

		mounted() {
          this.currentImage.setCss({
				transition: 'opacity '+ this.totalDuration +'ms '+ this.easing,
				opacity: 0
			});
		},

		destroyed() {
			this.currentImage.hide();

			this.currentImage.setCss({
				transition: 'none',
				opacity: 1
			});
		}
	};
</script>
