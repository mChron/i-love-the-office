<template>
  <div :class="['card', 'img-' + imgDirection, 'rounded-0']">
      <img
          :src="imgSrc"
          class="card-img rounded-0"
          :alt="'image of ' + altText"
      />
      <div class="card-body">
          <slot></slot>
      </div>
  </div>
</template>

<script>
    export default {
        name: "Card",
        props: ['imgDirection', 'imgSrc', 'altText']
    }
</script>

<style lang="scss">
.card {
    align-items: flex-start;
    &.img-left {
        flex-direction: row;
        .card-img {
            width: 33%;
        }
    }
    &.img-right {
        flex-direction: row-reverse;
        .card-img {
            width: 33%;
        }
    }
    &.img-bottom {
        flex-direction: column-reverse;
    }
}
</style>
