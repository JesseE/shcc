<template>
  <div class="animated-rect">
    <div class="animated-rect__rect" ref="smallRect"></div>
    <div class="animated-rect__rect" ref="largeRect"></div>
  </div>
</template>

<script>
import { TimelineMax, Power4 } from 'gsap/dist/gsap'

export default {
  name: 'animatedRect',
  mounted() {
    this.enlargeAnimation()
  },
  methods: {
    enlargeAnimation() {
      const tm = new TimelineMax();

      tm
        .to(this.$refs.largeRect, 1.6, {
          width: '100%',
          ease: Power4.easeInOut
        },)
        .to(this.$refs.smallRect, 2.6, {
          width: '80%',
          ease: Power4.easeInOut
        }, '-=1.8')
    }
  }
}
</script>
