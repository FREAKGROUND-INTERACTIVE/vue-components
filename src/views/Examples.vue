<template>
  <div class="example__back" v-on:click="$router.push('/')">
    <div class="example__back-icon">
      <div></div>
      <div></div>
    </div>
    <div class="example__back-text">HOME</div>
  </div>
  <Font-weight v-if="toShow == 'FontWeight'"></Font-weight>
  <Link-list v-if="toShow == 'LinkList'" :links="['1',2,'3']"></Link-list>
  
  <!-- <div class="example__no-component" v-else>no component yet</div> -->
</template>

<script>
import FontWeight from "@/components/examples/text/FontWeight";
import LinkList from "@/components/examples/menu_links/LinkList";
export default {
  props: {
    comp: String,
  },
  components: {
    FontWeight,
    LinkList,
  },
  watch: {
    comp: function (val) {
      this.toShow = val;
    },
  },
  data() {
    return {
      toShow: this.comp,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "./../assets/styles/setup";

.example__back {
  position: fixed;
  width: 40px;
  height: 40px;
  background-color: #333;
  overflow: hidden;
  cursor: pointer;
  @include transition(all 0.3s ease-in);

  .example__back-icon {
    position: relative;
    width: 40px;
    height: 40px;
    div {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 40%;
      height: 2px;
      background-color: white;
      @include transition(all 0.3s ease-in);

      // @include transform-origin(50% 50%);
      &:first-child {
        @include transform(translate(-50%, -50%) rotate(45deg));
      }

      &:last-child {
        @include transform(translate(-50%, -50%) rotate(-45deg));
      }
    }
  }

  .example__back-text {
    position: absolute;
    color: white;
    font-size: 10px;
    top: 50%;
    right: 20px;
    opacity: 0;
    pointer-events: none;
    @include transform(translateY(-50%));
    @include transition(all 0.2s ease-out);
  }

  &:hover {
    width: 85px;
    @include transition(all 0.3s ease-out);
    .example__back-icon {
      div:first-child {
        @include transform(translate(-50%, -50%) rotate(0));
        @include transition(all 0.5s ease-out);
      }

      div:last-child {
        @include transform(translate(-50%, -50%) rotate(0));
        @include transition(all 0.5s ease-out);
      }
    }

    .example__back-text {
      opacity: 1;
      @include transition(all 0.5s 0.3s ease-out);
    }
  }
}

.example__no-component {
  position: absolute;
  top: 50%;
  left: 50%;
  @include transform(translate(-50%, -50%));
}
</style>
