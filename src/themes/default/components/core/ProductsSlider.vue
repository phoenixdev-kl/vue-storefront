<template>
  <div class="collection">
    <div class="container">
      <div class="row center-xs">
        <header class="col-md-12">
          <h2 class="align-center cl-accent">
            {{ title }}
          </h2>
        </header>
      </div>
    </div>
    <div class="bg-cl-secondary collection-slider">
      <div class="container px15">
        <div class="row">
          <div class="col-md-12">
            <div class="center-xs cool-stuff-collection">
              <no-ssr>
                <carousel v-bind="config" @pageChange="setMuted">
                  <slide
                    v-for="product in products"
                    :key="product.id"
                  >
                    <product-tile
                      class="collection-product"
                      :product="product"
                      :labels-active="false"
                      :only-image="true"
                    />
                  </slide>
                </carousel>
              </no-ssr>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NoSSR from 'vue-no-ssr'
import ProductTile from 'theme/components/core/ProductTile'

export default {
  name: 'ProductsSlider',
  props: {
    title: {
      type: String,
      default: ''
    },
    products: {
      type: Array,
      required: true
    },
    config: {
      type: Object,
      required: true
    }
  },
  components: {
    'Carousel': () => import('vue-carousel').then(Slider => Slider.Carousel),
    'Slide': () => import('vue-carousel').then(Slider => Slider.Slide),
    ProductTile,
    'no-ssr': NoSSR
  },
  data () {
    return {
      currentPage: 0
    }
  },
  methods: {
    setMuted (currentPage) {
      this.currentPage = currentPage
    }
  }
}
</script>

<style lang="scss">
@import '~theme/css/variables/variables';
@import '~theme/css/helpers/functions/color';
$color-product-bg: color(secondary, $colors-background);

.collection-slider {
  overflow: hidden;
  .VueCarousel-wrapper {
    overflow: visible!important;
    &:before,
    &:after {
      content: "";
      height: 100%;
      position: absolute;
      top: 0;
      z-index: 1;
      display: none;

      @include media('o-screen', '>=xs') {
        display: block;
        width: calc((100vw - (#{map-get($breakpoints, 'xs') - $grid-flexbox-gutter-width} - 30px)) / 2);
      }

      @include media('o-screen', '>=sm') {
        width: calc((100vw - (#{map-get($breakpoints, 'sm') - $grid-flexbox-gutter-width} - 30px)) / 2);
      }

      @include media('o-screen', '>=md') {
        width: calc((100vw - (#{map-get($breakpoints, 'md') - $grid-flexbox-gutter-width} - 30px)) / 2);
      }

      @include media('o-screen', '>=lg') {
        width: calc((100vw - (#{map-get($breakpoints, 'lg') - $grid-flexbox-gutter-width} - 30px)) / 2);
      }
    }
    &:before {
      right: 100%;
      background: linear-gradient(to right, $color-product-bg 0%,$color-product-bg 40%,rgba($color-product-bg,0.2) 100%);
    }
    &:after {
      left: 100%;
      background: linear-gradient(to left, $color-product-bg 0%,$color-product-bg 40%,rgba($color-product-bg,0.2) 100%);
    }
  }
}

.product {
  &.collection-product {
    padding: 0;
  }
}

.collection-product {
  .product-link {
    display: block;
    padding: 0 15px;
  }

  .product-image {
    height: auto;
    will-change: opacity;

    img {
      max-width: 100%;
      max-height: 100%;
      height: auto;
      vertical-align: bottom;
    }
  }
}
</style>
