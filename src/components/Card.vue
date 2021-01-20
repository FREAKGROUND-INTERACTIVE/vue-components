<template>
  <div class="card" :class="{click: !comp}">
    <div class="card__header" :title="title">
      {{ title ? title : "no title" }}
      <div class="card__link">
        <router-link :to="{name:'Examples', params: {comp: comp}}" v-if="comp">Ir</router-link>
      </div>
    </div>
    <div class="card__content" :title="msn">
      {{ msn ? msn : "no msn" }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    msn: String,
    comp: String
  },
};
</script>

<style lang="scss" scoped>
.card {
  background-color: #ccc;
	min-width: 250px;
  max-width: 250px;
  margin-right: 1rem;
  .card__header {
    position: relative;
    text-transform: uppercase;
    font-weight: 900;
    background-color: #333;
    padding: 0.5rem;
    color: #ddd;
    .card__link {
      position: absolute;
      right: 0;
      top: 0;
      padding: 0.5rem;
      a:-webkit-any-link {
        color: #bbb;
      }
    }
  }
  .card__content {
		padding: 0.5rem;
    font-size: 12px;
    height: 46px;
  }
  &.click {
    cursor: pointer;
  }
}
</style>