<template>
  <div class="video-block-container"
    @mouseenter="showVideoControls"
    @mouseleave="defaultState"
  >
    <div class="video-block-bg"
        :class="{'video-block-bg--bright': !videoPaused}">
      <video class="video-block" ref="videoEl">
        <source src="../../assets/test-video.mp4" type="video/mp4" />
      </video>
    </div>
    <svg
      class="video-block__controls-arc"
      :class="{'video-block__controls-arc--hide' : !this.videoPaused  }"
      ref="videoBlockArc">
      <path ref="videoLengthArc" fill="none" />
      <path ref="videoCurrentLengthArc" fill="none" />
      <line ref="indicator" x1="155" x2="165" y1="130" y2="50" />
    </svg>
    <div class="video-block__controls"
         ref="videoControlsEl"
         @click="videoControl"
    >
      <playButton ref="playButtonEl" />
      <pauseButton ref="pauseButtonEl" />
    </div>
    <div
      class="video-block__text-container"
      :class="!videoPlayState ? 'is-hidden' : ''">
      <span ref="textContainer" class="video-block__text">RESUME</span>
    </div>
  </div>
</template>

<script>
import playButton from '../../images/icons/play-button-icon.svg';
import pauseButton from '../../images/icons/pause-button-icon.svg';
import { TimelineMax, TweenMax, Power4 } from 'gsap/dist/gsap';

export default {
  name: 'videoBlock',
  components: {
    playButton,
    pauseButton,
  },
  data() {
    return {
      videoStarted: false,
      videoPlayState: true,
      videoPaused: true
    }
  },
  mounted() {
    // 360 = 60.095 (this is the length of the video)
    // then a random value like  5.0 seconds in a video = 30 because 360 / 60 = 6 and 6 * 5.0 = 30
    this.setArc(359.99)
  },
  methods: {
    videoControl() {
      this.iconAnimation()

      this.videoPlayState
        ? this.playState() : this.pauseState()

      this.videoPlayState = !this.videoPlayState
    },
    playState() {
      this.$refs.videoEl.play(),
      this.videoPaused = false,
      this.videoStarted = true,
      this.hideVideoControls()
      this.textAnimation()
    },
    pauseState() {
      this.$refs.videoEl.pause(),
      this.setArc(
        (360/this.$refs.videoEl.duration)*this.$refs.videoEl.currentTime
      ),
      this.setIndicator(
        ((360/this.$refs.videoEl.duration)*this.$refs.videoEl.currentTime)
      ),
      this.videoPaused = true,
      this.videoStarted = true,
      this.showVideoControls()
      this.textAnimation()
    },
    setArc(circumfrence) {
      this.rotateAnimation(circumfrence)

      this.$refs.videoCurrentLengthArc
        .setAttribute("d", this.describeArc(150, 150, 100, -circumfrence, 0))


      if(!this.videoStarted)
        return this.$refs.videoLengthArc
          .setAttribute("d", this.describeArc(150, 150, 100, 0, circumfrence));
    },
    describeArc(x, y, radius, startAngle, endAngle) {
      const start = this.polarToCartesian(x, y, radius, endAngle);
      const end = this.polarToCartesian(x, y, radius, startAngle);

      const largeArcFlag = endAngle - startAngle <= 180 ? "0" : "1";

      const d = [
          "M", start.x, start.y,
          "A", radius, radius, 0, largeArcFlag, 0, end.x, end.y
      ].join(" ");

      return d;
    },
    polarToCartesian(centerX, centerY, radius, angleInDegrees) {
      const angleInRadians = (angleInDegrees-90) * Math.PI / 180.0;

      return {
        x: centerX + (radius * Math.cos(angleInRadians)),
        y: centerY + (radius * Math.sin(angleInRadians))
      };
    },
    setIndicator(circumfrenceDeg) {
      this.$refs.indicator
        .setAttribute('style', 'transform: rotate(-9deg); transform-origin: 50% 50%;')

      TweenMax.to(this.$refs.indicator, 0.3, {
        opacity: 1,
      })
    },
    defaultState() {
      if(this.videoStarted) return;

      const tm = new TimelineMax()

      tm
        .to(this.$refs.videoLengthArc, 0.3, {
          scale: 0.2,
          transformOrigin: "50% 50%",
          strokeWidth: '3px',
          opacity: 1
        })
        .to(this.$refs.videoLengthArc, 0.3, {
          scale: 1,
          transformOrigin: "50% 50%",
        }).to(this.$refs.videoControlsEl, 0.3, {
          opacity: 1
      })
    },
    rotateAnimation(circumfrence) {
      const tm = new TimelineMax()

      tm.to(this.$refs.videoBlockArc, 0.5, {
        rotate: `${circumfrence}_cw`,
        opacity: 1,
        ease: Power4.easeOut
      })
    },
    animateArcLength() {
      const tm = new TimelineMax()

      tm
        .to(this.$refs.videoLengthArc, 0.1, {
          opacity: 0
        })
        .to(this.$refs.videoCurrentLengthArc, 0.3, {
          opacity: 1,
          transformOrigin: "50% 50%"
        })
    },
    showVideoControls() {
      if(this.videoStarted && this.videoPaused) return this.animateArcLength()

      const tm = new TimelineMax()

      !this.videoStarted
      ?
        tm
         .to(this.$refs.videoCurrentLengthArc, 0.1, {
            opacity: 0,
            transformOrigin: "50% 50%" })
          .to(this.$refs.videoLengthArc, 0.3, {
            scale: 0.3,
            opacity: 0.3,
            transformOrigin: "50% 50%" })
          .to(this.$refs.videoLengthArc, 0.3, {
            scale: 0.4,
            transformOrigin: "50% 50%",
            strokeWidth: '100px',
            opacity: 0.5 })
          .to(this.$refs.videoControlsEl, 0.3, {
            scale: 1,
            transformOrigin: "50% 50%",
          })
      :
        tm
          .to(this.$refs.videoCurrentLengthArc, 0.1, {
            opacity: 0, })
          .to(this.$refs.indicator, 0.1, {
            opacity: 0, })
          .to(this.$refs.videoBlockArc, 0.1, {
            opacity: 1, })
          .to(this.$refs.videoControlsEl, 0.3, {
            scale: 1,
            transformOrigin: "50% 50%"})
          .fromTo(this.$refs.videoLengthArc, 0.3, {
            scale: 0.1,
            transformOrigin: "50% 50%",
            strokeWidth: '100px',
            opacity: 0},{scale: 0.4,
            transformOrigin: "50% 50%",
            strokeWidth: '100px',
            opacity: 0.5},'-=0.3')
    },
    hideVideoControls() {
      const tm = new TimelineMax()
        tm
          .to(this.$refs.videoControlsEl, 0.3, {
            scale: 0,
            transformOrigin: "50% 50%"})
          .to(this.$refs.videoBlockArc, 0.1, {
            opacity: 0,
          },'-=0.3')
    },
    iconAnimation() {
      const tm = new TimelineMax()

      this.videoPlayState
      ?
       tm
        .to(this.$refs.playButtonEl.$el, 0.1, {
          opacity: 0 })
        .to(this.$refs.pauseButtonEl.$el, 0.1, {
          opacity: 1 }).timeScale(2)
      :
        tm
          .to(this.$refs.playButtonEl.$el, 0.1, {
          opacity: 1 })
          .to(this.$refs.pauseButtonEl.$el, 0.1, {
          opacity: 0 }).timeScale(2)
    },
    textAnimation() {
      const tm = new TimelineMax()

      !this.videoPaused
      ?
        tm
          .to(this.$refs.textContainer, 0.3, {
          y: 0 })
      :
        tm
          .to(this.$refs.textContainer, 0.3, {
          y: -25 })
    }
  }
}
</script>
