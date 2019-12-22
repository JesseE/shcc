<template>
  <div class="page-title" ref="pageTitle">
    <div class="page-title__container"></div>
    <span class="page-title__small" ref="smallPageTitle">24/7 live.</span>
    <span class="page-title__large" ref="letterL">L</span>
    <div class="page-title__icon" ref="iconContainer">
      <div ref="pageTitleIcon">
        <loveIcon  />
      </div>
    </div>
    <span class="page-title__large">
      <span ref="letterV">V</span>
      <span ref="letterE">E .</span>
    </span>
    <span class="page-title__large--bottom">
      <span ref="secondLetterL">L .</span>
      <span ref="letterA">A .</span>
    </span>
  </div>
</template>

<script>
import loveIcon from '../../images/icons/heart.svg'
import { TimelineMax, Power4 } from 'gsap'

export default {
  name: 'pageTitle',
  components: {
    loveIcon
  },
  mounted() {
    const tm = new TimelineMax({delay: 0.7});
    const tmFast = new TimelineMax({delay: 1.7});

    tm
      .to(this.$refs.pageTitle,1, {
        opacity: 1,
        y: -10,
        ease: Power4.easeInOut
      })
      .to(this.$refs.smallPageTitle, 0.4, {
        y: -30
      },'-=1')
      .to(this.$refs.iconContainer, 1, {
        y: -50
      },'-=1')

    tmFast
      .timeScale(1)
      .to(this.$refs.pageTitleIcon, 0.5, {
      css: {
        className: '+=page-title__icon--blue'
      },
    })
    .to(this.$refs.pageTitleIcon, 0.5, {
      css: {
        className: '+=page-title__icon--red'
      },
    })
    .to(this.$refs.pageTitleIcon, 0.5, {
      css: {
        className: '+=page-title__icon--blue'
      },
    })
    .to(this.$refs.pageTitleIcon, 0.5, {
      css: {
        className: '+=page-title__icon--red'
      },
    }).to(this.$refs.pageTitleIcon, 0.5, {
      css: {
        className: '+=page-title__icon--blue'
      },
    })
    .to(this.$refs.pageTitleIcon, 1, {
      css: {
        className: '+=page-title__icon--red'
      },
    })


  }
}
</script>
