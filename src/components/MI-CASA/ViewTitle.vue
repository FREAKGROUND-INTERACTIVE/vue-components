<template>
  <div class="viewTitle">
    <h1>{{newTitle}}</h1>
    <h1>{{title}}</h1>
  </div>
</template>

<script>
export default {
  props: {
    text: String,
  },
  watch: {
    text: function (val) {
      this.newTitle = val;

      this.$el.classList.add("change");

      setTimeout(() => {
        this.title = this.newTitle;
        this.$el.classList.remove("change");
      }, 300);
    },
  },
  data() {
    return {
      title: this.text,
      newTitle: this.text
    };
  },
};
</script>

<style lang="scss" scoped>
@import "./../../assets/styles/setup";

.viewTitle {
  position: absolute;
  left: 50%;
  top: 50%;
  @include transform(translate(-50%, -50%));
  height: 140px;
  overflow: hidden;
  text-align: center;
  pointer-events: none;

  h1 {
    font-size: 10rem;
    text-transform: uppercase;
    @include transform(translateY(-100%));
    line-height: 1;
    color: white;
    font-weight: 900;
    white-space: nowrap;
  }

  &.change {
    h1 {
      @include transform(translateY(0));
      @include transition(all 0.3s ease-out);
    }
  }
}
</style>