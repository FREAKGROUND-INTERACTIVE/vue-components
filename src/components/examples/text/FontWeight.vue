<template>
  <div class="font">
    <template v-for="item in title" :key="item">
      <div class="font__phrase">
        <template v-for="char in item" :key="char">
          <div class="font__char">
            {{ char == " " ? "&nbsp;" : char }}
          </div>
        </template>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "this is\na title".split("\n"),
      delay: 100, //* miliseconds
    };
  },
  mounted() {
    const chars = this.$el.querySelectorAll(".font__char");
    console.log("chars: ", this.title);
    console.log("chars: ", chars);

    const divider = window.innerWidth / 9;
    document.addEventListener("mousemove", (e) => {
      // console.log(window.innerWidth, e);
      if (e.clientX <= divider) {
        [...chars].forEach((element, index) => {
          setTimeout(() => {
            this.weightAnimation(element, 100);
          }, this.delay * index);
        });
      }
      if (e.clientX >= divider && e.clientX <= divider * 2) {
        [...chars].forEach((element, index) => {
          setTimeout(() => {
            this.weightAnimation(element, 200);
          }, this.delay * index);
        });
      }
      if (e.clientX >= divider * 2 && e.clientX <= divider * 3) {
        [...chars].forEach((element, index) => {
          setTimeout(() => {
            this.weightAnimation(element, 300);
          }, this.delay * index);
        });
      }
      if (e.clientX >= divider * 3 && e.clientX <= divider * 4) {
        [...chars].forEach((element, index) => {
          setTimeout(() => {
            this.weightAnimation(element, 400);
          }, this.delay * index);
        });
      }
      if (e.clientX >= divider * 4 && e.clientX <= divider * 5) {
        [...chars].forEach((element, index) => {
          setTimeout(() => {
            this.weightAnimation(element, 500);
          }, this.delay * index);
        });
      }
      if (e.clientX >= divider * 5 && e.clientX <= divider * 6) {
        [...chars].forEach((element, index) => {
          setTimeout(() => {
            this.weightAnimation(element, 600);
          }, this.delay * index);
        });
      }
      if (e.clientX >= divider * 6 && e.clientX <= divider * 7) {
        [...chars].forEach((element, index) => {
          setTimeout(() => {
            this.weightAnimation(element, 700);
          }, this.delay * index);
        });
      }
      if (e.clientX >= divider * 7 && e.clientX <= divider * 8) {
        [...chars].forEach((element, index) => {
          setTimeout(() => {
            this.weightAnimation(element, 800);
          }, this.delay * index);
        });
      }
      if (e.clientX >= divider * 8) {
        [...chars].forEach((element, index) => {
          setTimeout(() => {
            this.weightAnimation(element, 900);
          }, this.delay * index);
        });
      }
    });
  },
  methods: {
    changeTitle() {},
    weightAnimation(elem, weight) {
      elem.style.fontWeight = weight;
      elem.style.fontSize = weight / 50 + 64 + "px";
      //   elem.style.color = (weight/100)
    },
    sizeAnimation(elem, index, size) {
      elem.style.fontSize = size + 64 + "px";
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./../../../assets/styles/setup";

.font {
  position: absolute;
  top: 50%;
  left: 50%;
  @include transform(translate(-50%, -50%));
  .font__phrase {
      display: flex;
      justify-content: center;
    .font__char {
      display: inline-block;
      font-size: 4rem;
      text-transform: uppercase;
      @include transition(all 0.5s);
    }
  }
}
</style>