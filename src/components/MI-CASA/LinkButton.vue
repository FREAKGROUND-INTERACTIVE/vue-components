<template>
  <transition v-on:enter="enter" v-bind:css="false">
    <div class="linkButton">
      <div class="linkButton__line">
        <div></div>
      </div>
      <router-link :to="linkUrl">
        <div class="linkButton__text">
          <template v-for="letter in text" :key="letter">
            <div class="linkButton__text-letter">
              {{ letter }}
            </div>
          </template>
        </div></router-link
      >
    </div>
  </transition>
</template>

<script>
import { gsap } from "gsap";

export default {
  props: {
    link: String,
  },
  watch: {
    link: function (val) {
      this.linkUrl = val;
    },
  },
  data() {
    return {
      linkUrl: this.link,
      text: "Next".split(""),
      letters: null,
    };
  },
  mounted() {
    this.letters = this.$el.querySelectorAll(".linkButton__text-letter");
    this.initAnimation();
  },
  methods: {
    enter: function () {
      console.log("enter");
    },
    initAnimation() {
      console.log("init");
      let animTl = gsap.timeline();
      this.letters.forEach((element) => {
        console.log(element);
        animTl.from(element, {
          duration: 1,
          y: "100%",
          // onComplete: function () {
          //   console.log(index);
          // },
        });
      });
      animTl.play();
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./../../assets/styles/setup";

.linkButton {
  position: absolute;
  left: 50%;
  top: 50%;
  @include transform(translate(-50%, -50%));

  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: center;

  .linkButton__line {
    margin-right: 1rem;

    div {
      width: 130px;
      height: 1px;
      background-color: #333;
    }
  }

  .linkButton__text {
    .linkButton__text-letter {
      display: inline-block;
    }
  }
}
</style>