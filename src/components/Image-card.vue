<template>
     <img :src="image['obj'].thumbnailUrl" alt="..." class="img-thumbnail">
</template>

<script>
export default {
  name: 'image-card',
  props: {
    image: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
  img {
    margin-bottom: 1.8rem;
  }
</style>
