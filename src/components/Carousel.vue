<template>
  <div class="c-carousel">
    <div class="c-carousel__wrapper">
      <div class="c-carousel__slides" :style="{'transform': `translateX(${currentOffset}%)`}">
        <slot />
      </div>
    </div>
    <div class="c-carousel__pagination" v-if="showPagination">
      <div class="c-carousel__pagination__item" v-for="(slide, index) in slides" :key="index"
        @click="goTo(index + 1)"
        :class="{ 'c-carousel__pagination__item--active': currentPage == (index + 1) }">
      </div>
    </div>
    <div class="c-carousel__navigation" v-if="showNavigation">
        <div class="c-carousel__navigation__item c-carousel__navigation__item--left" @click="onPrev" title="Previous">
          <svg class="icon icon-chevron-left">
            <use xlink:href="@/assets/icons/symbol-defs.svg#icon-chevron-left"></use>
          </svg>
        </div>
        <div class="c-carousel__navigation__item c-carousel__navigation__item--right" @click="onNext" title="Next">
          <svg class="icon icon-chevron-right">
            <use xlink:href="@/assets/icons/symbol-defs.svg#icon-chevron-right"></use>
          </svg>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Carousel',
  props: ['options'],
  data() {
    return {
      slides: [],
      currentOffset: 0,
      currentPage: 1,
      autoplay: true,
      autoplayTimer: 5000,
      autoplayInterval: undefined,
    }
  },
  methods: { 
    onNext() {
      this.clearAutoPlayInterval()
      
      if (this.currentPage > this.slideCount - 1) {
        this.currentOffset = 0
        this.currentPage = 1
      }
      else {
        this.currentOffset = this.currentPage * -100
        this.currentPage++
      }
    },
    onPrev() {
      this.clearAutoPlayInterval()

      if (this.currentPage == 1) {
        this.currentOffset = (this.slideCount - 1) * -100
        this.currentPage = this.slideCount
      }
      else {
        this.currentPage--
        this.currentOffset = (this.currentPage - 1) * -100
      }
    },
    goTo(slide) {
      if (this.currentPage == slide) return
      this.clearAutoPlayInterval()

      this.currentOffset = slide == 1 ? 0 : (slide - 1) * -100
      this.currentPage = slide
    },
    setAutoplayInterval() {
      this.autoplayInterval = setInterval(() => {
        this.onNext()
      }, this.autoplayTimer)
    },
    clearAutoPlayInterval() {
      if (this.autoplayInterval) {
        clearInterval(this.autoplayInterval)
        this.setAutoplayInterval()
      }
    }
  },
  mounted() {
    this.slides = this.$slots.default

    this.autoplay = this.options.autoplay != undefined ? this.options.autoplay : this.autoplay
    this.autoplayTimer = this.options.autoplayTimer ?? this.autoplayTimer
    if (this.autoplay) {
      this.setAutoplayInterval()
    }
  },
  computed: {
    slideCount: vm => vm.slides.length,
    showNavigation: vm => {
      let showNavigation = vm.options.showNavigation ?? true
      return vm.slideCount > 1 && showNavigation
    },
    showPagination: vm => {
      let showPagination = vm.options.showPagination ?? true
      return vm.slideCount > 1 && showPagination
    }
  }
}
</script>

<style lang="scss">
 .c-carousel {
   position: relative;
   
   &__wrapper {
    height: 100%;
    width: 100%;
    overflow: hidden;
   }

   &__slides {
     display: flex;
     transition: transform ease-in-out 450ms;
   }

   &__navigation {
     &__item {
       $self: &;
       cursor: pointer;
       height: 100%;
       top: 0;
       position: absolute;
       color: red;
       font-size: 2.5rem;
       padding: 0 1.5rem;
       color: white;
       opacity: .5;
       transition: all ease-in-out 150ms;

       .icon {
         position: relative;
         top: 50%;
         transform: translateY(-50%);
       }

       &#{ $self }--left:hover {
         background: linear-gradient(90deg, rgba(0,0,0, .25), transparent);
       }

       &#{ $self }--right {
         right: 0;

         &:hover {
           background: linear-gradient(90deg, transparent, rgba(0,0,0, .25));
         }
       }

       &:hover {
         opacity: 1;
       }
     }
   }

   &__pagination {
     position: absolute;
     display: flex;
     left: 50%;
     transform: translateX(-50%);
     bottom: 0;
     margin-bottom: 3rem;
     
     &__item {
       $self: &;
       cursor: pointer;
       margin: 0 .5rem;
       padding: .5rem;
       
       &::before {
         content: " ";
         display: block;
         height: .75rem;
         width: .75rem;
         background-color: white;
         border-radius: 50%;
         opacity: .5;
         transition: all ease-in-out 75ms;
         transform-origin: center;
       }

       &:hover::before {
         opacity: 1;
       }

       &#{ $self }--active::before {
         transform: scale(1.26);
         opacity: 1;
       }
     }
   }

   &::before {
     content: "";
     position: absolute;
     top: 0;
     bottom: 0;
     left: 0;
     right: 0;

     background-image: url(https://picsum.photos/1920/800);
     background-position: center;
     background-size: cover;

     filter: grayscale(60%) contrast(50%);
   }
 }
</style>