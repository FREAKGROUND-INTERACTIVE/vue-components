<template>
  <div class="link">
    <template v-for="item in links" :key="item">
      <!-- <div class="link__item">{{ item }}</div> -->
      <router-link
        class="link__item"
        :to="item.toString()"
        v-if="!isExternal"
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
</template>

<script>
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
    };
  },
  mounted() {
    let items = this.$el.querySelectorAll(".link__item");
    this.setSize(items);
    this.setColor(items);
  },
  methods: {
    setSize(items) {
      items.forEach((elem) => {
        elem.style.width = `${this.size ? this.size : 30}px`;
        elem.style.height = `${this.size ? this.size : 30}px`;
      });
    },
    setColor(items) {
      items.forEach((elem) => {
        elem.style.borderColor = `#${this.color ? this.color : "333"}`;
        elem.style.borderColor = `#${this.color ? this.color : "333"}`;
        elem.style.borderColor = `#${this.color ? this.color : "333"}`;
        elem.style.borderColor = `#${this.color ? this.color : "333"}`;
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./../../../assets/styles/setup";

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
    width: 30px;
    height: 30px;
    border-radius: 50%;
    border: 5px solid #333;
    //   margin: 0 2rem;
    @include transition(all 0.3s);

    cursor: pointer;

    &:hover {
      background-color: #ff0000;
    }
  }
}
</style>