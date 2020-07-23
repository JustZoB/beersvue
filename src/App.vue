
<template>
  <div id="app">
    <BeerList v-bind:list="list"></BeerList>
  </div>
</template>

<script>
const axios = require('axios');
import BeerList from './components/BeerList.vue'

export default {
  name: 'App',
  components: {
    BeerList
  },
  data () {
    return {
      list: []
    }
  },
  mounted() {
    axios
      .get('https://api.punkapi.com/v2/beers?page=1&limit=25')
      .then(response => {
        this.list = response.data
        console.log(this.list);
      })
  }
}
</script>

<style scoped>
#id {
  display: flex;
  justify-content: center;
}
</style>
