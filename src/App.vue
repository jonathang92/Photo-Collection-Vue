<template>
  <div id="app">
    <div class="container">
    <h1 class="display-4 text-center">Drag & Drop Images</h1>
      <draggable class="row" v-model="aImages"
      animation="400" @start="drag=true" @end="drag=false" >
       <div class="col-xl-2 col-md-2 col-lg-2 col-sm-6 col-6"
       v-for="(image, k) in aImages" :key="k">
       <div v-on:click="openModal(k)">
          <imagecard :image="image"></imagecard>
       </div>
        </div>
      </draggable>
  </div>
  <modal ref="modal"></modal>
  </div>
</template>
<style scoped lang="less">
  h1 {
    padding-bottom: 10px;
  }
</style>
<script>
import axios from 'axios';
import draggable from 'vuedraggable';
import imagecard from './components/Image-card.vue';
import modal from './components/Modal.vue';

export default {
  name: 'app',
  data() {
    return { images: Object, info: Object, aImages: [] };
  },
  components: {
    draggable,
    imagecard,
    modal,
  },
  mounted() {
    axios.get('https://jsonplaceholder.typicode.com/photos?albumId=1')
      .then((response) => {
        // JSON responses are automatically parsed.
        this.images = response.data;
        this.reorderImages();
      });
  },
  methods: {
    reorderImages() {
      Object.entries(this.images).forEach(([k]) => {
      // Get number of vowels
        const m = this.images[k].title.match(/[aeiou]/gi);
        this.aImages[k] = {
          id: this.images[k].id,
          lastName: (m === null) ? 0 : m.length,
          age: this.images[k],
        };
        this.aImages[k].id = this.images[k].id;
        this.aImages[k].id = this.images[k].id;
        this.aImages[k].count = (m === null) ? 0 : m.length;
        this.aImages[k].obj = this.images[k];
      });
      this.sortById();
      this.sortByCount();
    },
    sortById() {
      this.aImages.sort((a, b) => b.id - a.id);
    },
    // Sort by count value of array
    sortByCount() {
      this.aImages.sort((a, b) => a.count - b.count);
    },
    openModal(k) {
      this.$refs.modal.openModal(this.aImages[k].obj);
    },
  },
};
</script>

<style lang="less">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
