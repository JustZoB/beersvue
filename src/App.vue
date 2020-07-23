<template>
  <div id="app">
    <BeerList v-bind:list="list" @deleteBeer="deleteBeer"></BeerList>
    <ShowNext @next="next"></ShowNext>
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
      page: 1
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
      axios
        .get(`https://api.punkapi.com/v2/beers?page=${this.page}&limit=25`)
        .then(response => {
          this.list = this.list.concat(response.data);
        })
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
