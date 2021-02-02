<template>
  <div class="paragraph" :class="{left: align == 'left', right: align == 'right', center: align == 'center'}">
    <span class="paragraph__quote">{{ quote }}</span>
    <h2 class="paragraph__title">{{ title }}</h2>
    <h3 class="paragraph__subtitle">{{ subtitle }}</h3>
    <p class="paragraph__text">{{ text }}</p>
  </div>
</template>

<script>
export default {
  props: {
    quote: String,
    title: String,
    subtitle: String,
    text: String,
    align: String
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