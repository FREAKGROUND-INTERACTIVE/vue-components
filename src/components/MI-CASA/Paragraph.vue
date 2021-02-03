<template>
  <div
    class="paragraph"
    :class="{
      left: align == 'left',
      right: align == 'right',
      center: align == 'center',
    }"
  >
    <div class="paragraph__quote-container" v-if="quote">
      <div class="paragraph__quote">{{ quote }}</div>
    </div>
    <div class="paragraph__title-container">
      <h2 class="paragraph__title">{{ title }}</h2>
    </div>
    <div class="paragraph__subtitle-container" v-if="subtitle">
      <h3 class="paragraph__subtitle">{{ subtitle }}</h3>
    </div>
    <p class="paragraph__text">
      <template v-for="item in splitText" :key="item">
        <div class="paragraph__split-container">
          <div class="paragraph__split-text">
            {{ item }}
          </div>
        </div>
      </template>
    </p>
  </div>
</template>

<script>
import { gsap } from "gsap";

export default {
  props: {
    quote: String,
    title: String,
    subtitle: String,
    text: String,
    align: String,
  },
  data() {
    return {
      splitText: this.text.split(/\r?\n/),
    };
  },
  mounted() {
    this.initAnimation(1);
  },
  methods: {
    /**
     ** INIT-ANIMATION FUNCTION
     *? Function for animation when component is mounted
     * @param time time for animation duration
     */
    initAnimation(time) {
      let lines = document.querySelectorAll(".paragraph__split-text");
      lines = Array.prototype.slice.call(lines, 0);

      let initTl = gsap.timeline();
      if (this.quote) {
        initTl.from(".paragraph__quote", {
          duration: time,
          // delay: delay,
          y: "100%",
          ease: "power1.inOut"
        });
      }

      initTl.from(".paragraph__title", {
        duration: time,
        // delay: delay,
        y: "100%",
        ease: "power1.inOut"
      });

      if (this.subtitle) {
        initTl.from(".paragraph__subtitle", {
          duration: time,
          // delay: delay,
          y: "100%",
          ease: "power1.inOut"
        });
      }

      lines.forEach((element) => {
        initTl.from(element, {
          duration: time,
          y: "100%",
          ease: "power1.inOut"
        }, "<0.2");
      });

      initTl.play();
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./../../assets/styles/setup";

.paragraph {
  position: absolute;
  left: 50%;
  top: 50%;

  @include transform(translate(-50%, -50%));

  .paragraph__quote-container,
  .paragraph__subtitle-container,
  .paragraph__title-container {
    overflow: hidden;
  }

  .paragraph__quote {
    font-family: $lora;
    font-size: 14px;
    font-weight: 400;
  }

  .paragraph__subtitle {
    font-family: $lora;
    font-size: 14px;
    font-weight: 400;
    margin-top: 0.5rem;
  }

  .paragraph__title {
    font-family: $lora;
    font-size: 24px;
    font-weight: 400;
    color: $red;
    margin-top: 0.5rem;
  }

  .paragraph__text {
    font-family: $fira;
    font-size: 16px;
    font-weight: 300;
    margin-top: 2rem;

    .paragraph__split-container {
      overflow: hidden;
    }
  }

  &.left {
    text-align: left;
  }

  &.right {
    text-align: right;
  }

  &.center {
    text-align: center;
  }
}
</style>