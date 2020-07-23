<template>
  <div id="app">
    <BeerList v-bind:list="list" @deleteBeer="deleteBeer"></BeerList>
    <ShowNext @next="next" v-bind:style="styleShowNext" v-bind:buttonText="buttonText"></ShowNext>
    <Overlay @applyEdit="applyEdit"></Overlay>
  </div>
</template>

<script>
const axios = require('axios');
import BeerList from './components/BeerList.vue'
import ShowNext from './components/ShowNext.vue'
import Overlay from './components/Overlay.vue'

export default {
  name: 'App',
  components: {
    BeerList,
    Overlay,
    ShowNext
  },
  data () {
    return {
      list: [],
      page: 1,
      buttonText: 'Show Text',
      styleShowNext: { display: 'flex' }
    }
  },
  mounted() {
    axios
      .get('https://api.punkapi.com/v2/beers?page=1&limit=25')
      .then(response => {
        this.list = response.data
      })
  },
  methods: {
    deleteBeer(id) {
      this.list = this.list.filter(t => t.id !== id)
    },
    next() {
      this.page++;
      this.buttonText = "Loading.."
      axios
        .get(`https://api.punkapi.com/v2/beers?page=${this.page}&limit=25`)
        .then(response => {
          if (response.data.length != 0) {
            this.list = this.list.concat(response.data);
          } else {
            this.styleShowNext = { display: 'none' };
          }
        });
      this.buttonText = "Show Text"
    },
    applyEdit(id, name, description) {
      this.list[id - 1].name = name;
      this.list[id - 1].description = description;
    }
  }
}
</script>

<style scoped>

</style>
