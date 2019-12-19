<template>
  <article class="page-article">
    <div class="page-article__text-block" ref="articleTextBlock">
      <h2 class="page-article__title">Spring <span class="page-article__title page-article__title--red">2017</span></h2>
      <h3 class="page-article__subtitle">With Anwar Hadid &amp; Sophia Richie</h3>
      <span class="page-article__description">
        Engineered for perfect form and exeptional fit - whatever you do in them.
      </span>
      <button class="page-article__button">
        <span class="page-article__button-text">
          View all Products
        </span>
      </button>
    </div>
    <div class="page-article__image-container" ref="articleImage">
      <img src="../../images/tommy-denim__header-men.jpg"/>
    </div>
    <div class="animated-block">
      <div class="animated-rectangle--large" ref="largeRect"></div>
      <div class="animated-rectangle" ref="smallRect"></div>
    </div>
  </article>
</template>

<script>
import { TimelineMax, Power3 } from 'gsap'

export default {
  name: 'pageArticle',
  mounted() {
    this.animateRect(Power3.easeInOut)
  },
  methods: {
    animateRect(ease) {
      const tm = new TimelineMax();

      tm
      .to( this.$refs.articleTextBlock,
        0.8, {
        opacity: 1,
        ease:ease
      })
      .to(this.$refs.articleImage,
        1,{
        opacity: 1,
        ease:ease
      }, '-=0.8')
      .to(this.$refs.largeRect,
        1.2,{
        width: '5vw',
        ease:ease
      }, '-=1.2')
      .to(this.$refs.smallRect,
        1.2,{
        width: '0vw',
        ease:ease
      }, '-=1.2')
    }
  }
}
</script>

<style>

</style>
