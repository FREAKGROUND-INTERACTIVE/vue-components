<template>
  <div class="button">
    <div class="button__title">Hello Baby!</div>
    <div class="button__line"></div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
@import "./../../assets/styles/setup";

.button {
  position: absolute;
  left: 50%;
  top: 50%;
  @include transform(translate(-50%, -50%));
  cursor: pointer;

  .button__title {


    &:after {
      content: "+";
      margin-left: 0.2rem;
      display: inline-block;
      @include transform(rotate(0deg));

      @include transition(all 1s ease-in);
    }
  }

  .button__line {
    margin-top: 0.4rem;
    width: 100%;
    height: 1px;
    background-color: #333;
    @include transition(width 1s ease-in);
  }

  &:hover {
    .button__line {
      width: 10%;
      @include transition(width 0.5s ease-in);
    }

    .button__title {
      animation-name: text;
      animation-duration: 2s;

      &:after {
        @include transform(rotate(45deg));

        @include transition(all 0.5s ease-in);
      }
    }
  }
}
// keyframes animations

@keyframes text {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>