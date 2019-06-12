<template>
    <div id="app">
        <div class="container mx-auto">
            <div class="">
                <div class="">
                    <vue-hsl-slide style="width: 768px;height: 432px" :options="fluxOptions" :images="fluxImages"
                                   :transitions="fluxTransitions" :captions="fluxCaptions" ref="slider">
                        <!--						<flux-caption slot="caption"></flux-caption>-->
                        <!--						<flux-controls slot="controls"></flux-controls>-->
                        <!--						<flux-index slot="index"></flux-index>-->
                        <!--						<flux-pagination slot="pagination"></flux-pagination>-->
                    </vue-hsl-slide>
                </div>
                <div class="transitions">
                    <h4 class="mb-2">2D Transitions</h4>

                    <ul class="list-reset flex mb-2">
                        <li class="flex-1 mr-2">
                            <a :class="transitionClass('transitionFade')" @click="showNext('transitionFade')">Fade</a>
                        </li>

                        <!--						<li class="flex-1">-->
                        <!--							<a :class="transitionClass('transitionKenburn')" @click="showNext('transitionKenburn')">Kenburn</a>-->
                        <!--						</li>-->
                    </ul>

                    <ul class="list-reset flex mb-2">
                        <li class="flex-1 mr-2">
                            <a :class="transitionClass('transitionSwipe')"
                               @click="showNext('transitionSwipe')">Swipe</a>
                        </li>

                        <li class="flex-1">
                            <a :class="transitionClass('transitionSlide')"
                               @click="showNext('transitionSlide')">Slide</a>
                        </li>
                    </ul>

                    <ul class="list-reset flex mb-2">
                        <li class="flex-1 mr-2">
                            <a @click="showNext('transitionWaterfall')" :class="transitionClass('transitionWaterfall')">Waterfall</a>
                        </li>

                        <li class="flex-1 mr-2">
                            <a @click="showNext('transitionZip')" :class="transitionClass('transitionZip')">Zip</a>
                        </li>

                        <li class="flex-1">
                            <a @click="showNext('transitionBlinds2d')" :class="transitionClass('transitionBlinds2d')">Blinds
                                2D</a>
                        </li>
                    </ul>

                    <ul class="list-reset flex mb-2">
                        <li class="flex-1 mr-2">
                            <a @click="showNext('transitionBlocks1')" :class="transitionClass('transitionBlocks1')">Blocks
                                1</a>
                        </li>

                        <li class="flex-1">
                            <a @click="showNext('transitionBlocks2')" :class="transitionClass('transitionBlocks2')">Blocks
                                2</a>
                        </li>
                    </ul>

                    <ul class="list-reset flex mb-2">
                        <li class="flex-1 mr-2">
                            <a @click="showNext('transitionConcentric')"
                               :class="transitionClass('transitionConcentric')">Concentric</a>
                        </li>

                        <li class="flex-1 mr-2">
                            <a @click="showNext('transitionWarp')" :class="transitionClass('transitionWarp')">Warp</a>
                        </li>

                        <li class="flex-1">
                            <a @click="showNext('transitionCamera')"
                               :class="transitionClass('transitionCamera')">Camera</a>
                        </li>
                    </ul>

                    <h4 class="mt-5 mb-2">3D Transitions</h4>

                    <ul class="list-reset flex mb-2">
                        <li class="flex-1 mr-2">
                            <a :class="transitionClass('transitionCube')" @click="showNext('transitionCube')">Cube</a>
                        </li>

                        <li class="flex-1 mr-2">
                            <a @click="showNext('transitionBook')" :class="transitionClass('transitionBook')">Book</a>
                        </li>

                        <li class="flex-1">
                            <a @click="showNext('transitionFall')" :class="transitionClass('transitionFall')">Fall</a>
                        </li>
                    </ul>

                    <ul class="list-reset flex mb-2">
                        <li class="flex-1 mr-2">
                            <a @click="showNext('transitionWave')" :class="transitionClass('transitionWave')">Wave</a>
                        </li>

                        <li class="flex-1">
                            <a @click="showNext('transitionBlinds3d')" :class="transitionClass('transitionBlinds3d')">Blinds
                                3D</a>
                        </li>
                    </ul>

                    <ul class="list-reset flex">
                        <li class="flex-1 mr-2">
                            <a @click="showNext('transitionRound1')" :class="transitionClass('transitionRound1')">Round
                                1</a>
                        </li>

                        <li class="flex-1 mr-2">
                            <a @click="showNext('transitionRound2')" :class="transitionClass('transitionRound2')">Round
                                2</a>
                        </li>

                        <li class="flex-1">
                            <a @click="showNext('transitionExplode')" :class="transitionClass('transitionExplode')">Explode</a>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
  import VueHslSlide from './components/VueHslSlide.vue';
  import FluxCaption from './components/FluxCaption.vue';
  import FluxControls from './components/FluxControls.vue';
  import FluxIndex from './components/FluxIndex.vue';
  import FluxPagination from './components/FluxPagination.vue';
  import Transitions from './components/transitions/index.js';
  import FluxParallax from './components/FluxParallax.vue';

  export default {
    name: 'app',

    components: {
      VueHslSlide,
      // FluxCaption,
      // FluxControls,
      // FluxIndex,
      // FluxPagination,
      // FluxParallax
    },

    data: () => ({
      rendered: false,
      baseTransitionClass: 'text-center whitespace-no-wrap block border border-grey-light rounded text-white cursor-pointer py-2 px-4 shadow-md',
      activeTransitionClass: 'bg-black',
      inactiveTransitionClass: 'bg-grey-darkest hover:bg-black',
      fluxOptions: {
        autoplay: true,
        bindKeys: true,
        fullscreen: true,
        delay: 1000,
        duration: 1000,
        img_width: 768,
        img_height: 432,
      },
      fluxImages: [
        'https://newmedia.hesiling.com/img/OwInifzx9spi9gXpFipjyJOJ4DyynoBexJy4eKPI.png',
        'https://newmedia.hesiling.com/img/3WItsU2zKhrInPOzL0e4QhlFY8Ra8GuLpSbrn3Xm.png',
        'https://newmedia.hesiling.com/img/OwInifzx9spi9gXpFipjyJOJ4DyynoBexJy4eKPI.png',
        'https://newmedia.hesiling.com/img/3WItsU2zKhrInPOzL0e4QhlFY8Ra8GuLpSbrn3Xm.png',
        // 'slides/sy222.jpeg',
        // 'slides/sy333.jpeg',
        // 'slides/sy444.jpeg',
        // 'https://newmedia.hesiling.com/img/G2KXwnrfEv6YC9FWTEVFFhnPtRoLPVI8i8IZLyYF.png',
        // 'https://newmedia.hesiling.com/img/uQG9SpG2ePc3boe96mbt74wfeYvEH4E5ZfNmayP7.jpeg',
        // 'https://newmedia.hesiling.com/img/bR15k0MK1kt1p0j9fMBUXTGXtnrqI15LaEt8L81R.jpeg'
      ],
      fluxTransitions: Transitions,
      fluxCaptions: ['First caption', 'Second caption', undefined, 'Fourth caption']
    }),

    computed: {
      currentTransition: function () {
        if (!this.rendered || !this.$refs.slider || !this.$refs.slider.transition)
          return undefined;

        return this.$refs.slider.transition.current;
      }
    },

    mounted() {
      this.rendered = true;
    },

    methods: {
      showNext(transition) {
        this.$refs.slider.showImage('next', transition);
      },

      transitionClass(transition) {
        let tClass = this.baseTransitionClass;

        if (this.currentTransition === transition)
          tClass += ' ' + this.activeTransitionClass;

        else
          tClass += ' ' + this.inactiveTransitionClass;

        return tClass;
      }
    }
  }
</script>

<style lang="scss" scoped>
    #app {
        margin-top: 50px;
    }

    .vue-flux {
        box-shadow: 0 0 12px 2px rgba(34, 36, 38, .85);
    }

    .transitions a {
        font-size: .975rem;
    }

    .flux-parallax {
        position: relative;
        font-size: 3rem;
        color: white;
        font-weight: bold;
        justify-content: center;
        align-items: center;
        text-shadow: -2px -2px 0 black,
        2px -2px 0 black,
        -2px 2px 0 black,
        2px 2px 0 black;
    }

    p {
        margin: 24px 0;
    }
</style>
