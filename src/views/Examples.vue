<template>
  <div class="example__back" v-on:click="$router.push('/')">
    <div class="example__back-icon">
      <div></div>
      <div></div>
    </div>
    <div class="example__back-text">HOME</div>
  </div>
  <Font-weight v-if="toShow == 'FontWeight'"></Font-weight>
  <Links-list v-if="toShow == 'LinksList'" :links="['1',2,'3']"></Links-list>
  <Bread-crumb v-if="toShow == 'BreadCrumb'" :number="numberPage" :title="titlePage"></Bread-crumb>
  
  <!-- <div class="example__no-component" v-else>no component yet</div> -->
</template>

<script>
import FontWeight from "@/components/MI-CASA/FontWeight";
import LinksList from "@/components/MI-CASA/LinksList";
import BreadCrumb from "@/components/MI-CASA/BreadCrumb";
export default {
  props: {
    comp: String,
  },
  components: {
    FontWeight,
    LinksList,
    BreadCrumb
  },
  watch: {
    comp: function (val) {
      this.toShow = val;
    },
  },
  data() {
    return {
      toShow: this.comp,
      numberPage: "01",
      titlePage: "Agency",
    };
  },
  mounted() {
    setTimeout(() => {
      this.titlePage = "Studio";
      this.numberPage = "02";
    }, 3000);
  }
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
