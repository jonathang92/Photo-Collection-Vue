<template>
    <b-modal id="modalDetail" ok-only>
        <img :src="url" class="rounded mx-auto d-block img-fluid" alt="Responsive image">
        <template v-slot:modal-footer>
          <p>{{title}}</p>
        </template>
    </b-modal>
</template>

<script>
export default {
  name: 'modal',
  data() {
    return { url: '', title: '' };
  },
  methods: {
    openModal(image) {
      this.url = image.url;
      this.title = image.title;
      this.$root.$emit('bv::show::modal', 'modalDetail', '#btnShow');
    },
  },

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
  p {
      text-align: right;
  }
</style>
