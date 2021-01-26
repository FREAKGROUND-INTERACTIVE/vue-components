<template>
  <div class="linkButton">
    <div class="linkButton__line">
      <div></div>
    </div>
    <router-link :to="linkUrl"><div class="linkButton__text">Next</div></router-link>
  </div>
</template>

<script>
  export default {
    props: {
      link: String
    },
    watch: {
      link: function(val) {
        this.linkUrl = val;
      }
    },
    data() {
      return {
        linkUrl: this.link 
      }
    }
  }
</script>

<style lang="scss" scoped>
@import "./../../assets/styles/setup";

.linkButton {
  position: absolute;
  left: 50%;
  top: 50%;
  @include transform(translate(-50%, -50%));

  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: center;

  .linkButton__line {
    margin-right: 1rem;
    
    div {
      width: 130px;
      height: 1px;
      background-color: #333;
    }
  }
}

</style>