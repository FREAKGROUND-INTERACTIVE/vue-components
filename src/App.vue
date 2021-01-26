<template>
  <router-view />
  <!--* cateories slider -->
  <transition name="slider">
    <div
      class="slider__container"
      v-if="slider"
      :class="{ inComponent: !showCategories }"
    >
      <transition name="back">
        <div
          class="slider__back"
          v-on:click="showCategories = true"
          v-if="!showCategories"
        >
          <i class="material-icons">arrow_circle_up</i>
        </div>
      </transition>
      <template v-for="card in categories" :key="card.title">
        <div v-on:click="getComponents(card.components)" v-if="showCategories">
          <Card :title="card.title" :msn="card.msn" />
        </div>
      </template>
      <template v-for="card in cards" :key="card.title">
        <Card
          :title="card.title"
          :msn="card.msn"
          :comp="card.comp"
          v-if="!showCategories"
        />
      </template>
    </div>
  </transition>
  <!--* show/hide categories -->
  <div class="slider__show" v-on:click="slider = !slider">
    <transition name="btn">
      <p v-if="!slider">show</p>
    </transition>
    <transition name="btnHide">
      <p v-if="slider">hide</p>
    </transition>
  </div>
</template>

<script>
import Card from "@/components/Card";
export default {
  components: {
    Card,
  },
  data() {
    return {
      slider: false,
      showCategories: true,
      categories: [
        {
          title: "MI-CASA",
          msn: "Developed components for MI-CASA web project",
          components: [
            {
              title: "links list",
              msn: "circle list for menu links",
              comp: "LinksList"
            },
            {
              title: "font weight",
              msn: "font weight animation with mouseX position",
              comp: "FontWeight"
            },
            {
              title: "breadcrumb",
              msn: "actual state for views",
              comp: "BreadCrumb"
            },
            {
              title: "button",
              msn: "general button",
              comp: "Button"
            },
            {
              title: "link button",
              msn: "button for links",
              comp: "LinkButton"
            },
            {
              title: "img view title",
              msn: "img for the main title view",
              comp: "ImgViewTitle"
            },
            {
              title: "view title",
              msn: "title for the main title view",
              comp: "ViewTitle"
            },
          ],
        }
      ],
      cards: [],
    };
  },
  methods: {
    getComponents(components) {
      this.cards = components;
      this.showCategories = false;
    },
  },
};
</script>

<style lang="scss">
@import "./assets/styles/setup";

.slider__container {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: #ddd;
  padding: 1rem;

  display: flex;
  @include transition(all 0.3s);

  .slider__back {
    position: absolute;
    top: 0;
    left: 0;
    width: 45px;
    height: 100%;
    background-color: #333;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    @include transition(all 0.3s);

    i {
      color: white;
      @include transform(rotate(-90deg));
      @include transition(all 0.3s);
    }

    &:hover {
      background-color: #ddd;
      @include transition(all 0.3s);
      i {
        color: #333;
        @include transition(all 0.3s);
      }
    }
  }

  &.inComponent {
    padding-left: 60px;
  }
}

.slider__show {
  position: fixed;
  bottom: 0;
  right: 0;
  width: 50px;
  height: 30px;
  background-color: #333;
  cursor: pointer;
  overflow: hidden;

  p {
    position: absolute;
    width: 100%;
    font-size: 10px;
    text-align: center;
    color: white;
    padding-top: 0.5rem;
  }
}

//* ANIMATION TRANSITION

//? SLIDER ANIMATION
.slider-enter-active {
  @include transform(translateY(100%));
  @include transition(all 0.5s ease-out);
}
.slider-enter-to {
  @include transform(translateY(0));
  // opacity: 1;
}

.slider-leave {
  @include transform(translateY(0));
  opacity: 1;
}
.slider-leave-to {
  @include transform(translateY(100%));
  // opacity: 0;
}
.slider-leave-active {
  @include transition(all 0.5s ease-in);
}

//? BTN ANIMATION
.btn-enter-active {
  @include transform(translateY(200%));
  @include transition(all 0.5s ease-out);
}
.btn-enter-to {
  @include transform(translateY(0));
  // opacity: 1;
}

.btn-leave {
  @include transform(translateY(0));
  // opacity: 1;
}
.btn-leave-to {
  @include transform(translateY(200%));
  // opacity: 0;
}
.btn-leave-active {
  @include transition(all 0.5s ease-in);
}

//? BTN 2 ANIMATION
.btnHide-enter-active {
  @include transform(translateY(-200%));
  @include transition(all 0.5s ease-out);
}
.btnHide-enter-to {
  @include transform(translateY(0));
  // opacity: 1;
}

.btnHide-leave {
  @include transform(translateY(0));
  // opacity: 1;
}
.btnHide-leave-to {
  @include transform(translateY(-200%));
  // opacity: 0;
}
.btnHide-leave-active {
  @include transition(all 0.5s ease-in);
}

//? BACK BTN ANIMATION
.back-enter-active {
  @include transform(translateX(-100%));
  @include transition(all 0.5s ease-out);
}
.back-enter-to {
  @include transform(translateX(0));
  // opacity: 1;
}

.back-leave {
  @include transform(translateX(0));
  // opacity: 1;
}
.back-leave-to {
  @include transform(translateX(-100%));
  // opacity: 0;
}
.back-leave-active {
  @include transition(all 0.5s ease-in);
}
</style>
