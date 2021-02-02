<template>
  <div class="clientList">
    <div v-for="client in list" :key="client">
      <img :src="client" alt="Clients" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    list: Array
  },
};
</script>

<style lang="scss" scoped>
@import "./../../assets/styles/setup";

.clientList {
  position: absolute;
  left: 50%;
  top: 50%;
  @include transform(translate(-50%, -50%));
  display: grid;
  grid-template-columns: auto auto auto auto auto;

  div {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: grey;
    width: 170px;
    height: 85px;
    margin: 0.1rem;

    img {
      width: 75%;
      height: 75%;
    }
  }
}
</style>