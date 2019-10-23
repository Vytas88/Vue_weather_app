<template>
  <div
    :class="['favorite-icon', { 'favorite-icon--active': active }]"
    @click="$emit('click', $event)"
  >{{ active ? '★' : '✰' }}</div>
</template>
<script>
export default {
  name: "FavoriteIcon",
  props: {
    active: {
      type: Boolean,
      default: false
    }
  }
};
</script>
<style lang="scss">
.favorite-icon {
  height: 36px;
  width: 50px;
  display: flex;
  position: absolute;

  padding-left: 250px;
  &--active {
    color: yellow;
  }
  cursor: pointer;
}
</style>