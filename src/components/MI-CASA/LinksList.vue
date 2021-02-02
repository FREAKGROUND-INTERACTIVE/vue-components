<template>
  <transition v-on:leave="leave" v-bind:css="false">
    <div class="link">
      <template v-for="item in links" :key="item">
        <!-- <div class="link__item">{{ item }}</div> -->
        <router-link
          class="link__item"
          :to="item.toString()"
          v-if="!isExternal"
          @mouseenter="setTitle(item.toString())"
        ></router-link>
        <a
          :href="item.toString()"
          target="_blank"
          rel="noopener noreferrer"
          class="link__item"
          v-if="isExternal"
        ></a>
      </template>
    </div>
  </transition>
</template>

<script>
import { gsap } from "gsap";

export default {
  props: {
    links: Array,
    external: Boolean,
    size: Number,
    color: String,
  },
  data() {
    return {
      isExternal: this.external ? true : false,
      items: null,
    };
  },
  mounted() {
    this.items = this.$el.querySelectorAll(".link__item");
    this.setSize(this.items);
    this.setColor(this.items);
  },
  methods: {
    setSize(items) {
      items.forEach((elem, index) => {
        gsap.to(elem, {
          duration: 0.5,
          width: "15px",
          height: "15px",
          delay: index * 0.5,
        });
      });
    },
    setColor(items) {
      items.forEach((elem) => {
        elem.style.borderColor = `#${this.color ? this.color : "fff"}`;
        elem.style.borderColor = `#${this.color ? this.color : "fff"}`;
        elem.style.borderColor = `#${this.color ? this.color : "fff"}`;
        elem.style.borderColor = `#${this.color ? this.color : "fff"}`;
      });
    },
    setTitle(title) {
      this.$emit("changeTitle", title);
    },
    leave:function(done) {
      this.exitAnimation(done);
      console.log('Se fue');
    },
    exitAnimation(done) {
      this.items.forEach((elem, index) => {
        gsap.to(elem, {
          duration: 0.5,
          width: 0,
          height: 0,
          delay: index * 0.5,
          onComplete: function() {
            done();
          },
        });
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./../../assets/styles/setup";

.link {
  //* for this vue
  position: absolute;
  top: 50%;
  left: 50%;
  @include transform(translate(-50%, -50%));
  //* end for this vue

  width: 100%;
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;

  .link__item {
    width: 0;
    height: 0;
    border-radius: 50%;
    border: 1px solid #fff;
    //   margin: 0 2rem;
    @include transition(all 0.6s ease-out);

    cursor: pointer;

    &:hover {
      background-color: #fff;
      width: 25px !important;
      height: 25px !important;
    }
  }
}
</style>