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
  <Bread-crumb v-if="toShow == 'BreadCrumb'" :number="numberPage" :title="titlePage" :pages="[1, 2, 3, 4, 5, 6]"></Bread-crumb>
  <Button v-if="toShow == 'Button'"></Button>
  <Link-button :link="link" v-if="toShow == 'LinkButton'"></Link-button>
  <Img-view-title v-if="toShow == 'ImgViewTitle'"></Img-view-title>
  <View-title v-if="toShow == 'ViewTitle'" :text="titlePage"></View-title>
  <Home3d v-if="toShow == 'Home3d'"></Home3d>
  <Paragraph v-if="toShow == 'Paragraph'" :align="'left'" :quote="'Example quote'" :title="'Mi Casa Studios'" :subtitle="'Example subtitle'" :text="' Lorem\n ipsum dolor sit amet consectetur, adipisicing elit.\n Rerum blanditiis dolores earum adipisci dolore ut consectetur, illum dolorem maxime modi praesentium officia\n ratione sed laborum in voluptate incidunt, minus ex?'"></Paragraph>
  <Services v-if="toShow == 'Services'" :list="servicesList"></Services>
  <Brand-header v-if="toShow == 'BrandHeader'" :link="link"></Brand-header>
  <Client-list v-if="toShow == 'ClientList'" :list="clientList"></Client-list>
  
  <!-- <div class="example__no-component" v-else>no component yet</div> -->
</template>

<script>
import FontWeight from "@/components/MI-CASA/FontWeight";
import LinksList from "@/components/MI-CASA/LinksList";
import BreadCrumb from "@/components/MI-CASA/BreadCrumb";
import Button from "@/components/MI-CASA/Button";
import LinkButton from "@/components/MI-CASA/LinkButton";
import ImgViewTitle from "@/components/MI-CASA/ImgViewTitle";
import ViewTitle from "@/components/MI-CASA/ViewTitle";
import Home3d from "@/components/MI-CASA/Home3d";
import Paragraph from "@/components/MI-CASA/Paragraph";
import Services from "@/components/MI-CASA/Services";
import BrandHeader from "@/components/MI-CASA/BrandHeader";
import ClientList from "@/components/MI-CASA/ClientList";

export default {
  props: {
    comp: String,
  },
  components: {
    FontWeight,
    LinksList,
    BreadCrumb,
    Button,
    LinkButton,
    ImgViewTitle,
    ViewTitle,
    Home3d,
    Paragraph,
    Services,
    BrandHeader,
    ClientList
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
      link: "/",
      servicesList: ['Service 1', 'Service 2', 'Service 3','Service 1', 'Service 2', 'Service 3','Service 1', 'Service 2', 'Service 3',],
      clientList: ['https://picsum.photos/1920/1080?random=1','https://picsum.photos/1920/1080?random=2','https://picsum.photos/1920/1080?random=3','https://picsum.photos/1920/1080?random=4','https://picsum.photos/1920/1080?random=5','https://picsum.photos/1920/1080?random=1','https://picsum.photos/1920/1080?random=2','https://picsum.photos/1920/1080?random=3','https://picsum.photos/1920/1080?random=4','https://picsum.photos/1920/1080?random=5','https://picsum.photos/1920/1080?random=1','https://picsum.photos/1920/1080?random=2','https://picsum.photos/1920/1080?random=3','https://picsum.photos/1920/1080?random=4','https://picsum.photos/1920/1080?random=5','https://picsum.photos/1920/1080?random=1','https://picsum.photos/1920/1080?random=2','https://picsum.photos/1920/1080?random=3','https://picsum.photos/1920/1080?random=4','https://picsum.photos/1920/1080?random=5']
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
