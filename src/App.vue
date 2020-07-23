
<template>
  <div id="app">
    <BeerList v-bind:list="list" @deleteBeer="deleteBeer"></BeerList>
    <ShowNext @next="next"></ShowNext>
  </div>
</template>

<script>
const axios = require('axios');
import BeerList from './components/BeerList.vue'
import ShowNext from './components/ShowNext.vue'

export default {
  name: 'App',
  components: {
    BeerList,
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
    }
  }
}
</script>

<style scoped>
#id {
  display: flex;
  justify-content: center;
}
</style>
