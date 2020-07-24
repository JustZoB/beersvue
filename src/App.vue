<template>
  <div id="app">
    <div class="beerlist">
      <Beer 
        v-for="elem of list" 
        :key="elem.id"
        :elem="elem"
        @remove="removeBeer"
        @edit="startEdit"
      />
    </div>
    <div class="next" v-show="visibleShowNext">
      <button class="next__button" @click="next" :buttonText="buttonText">
        {{ buttonText }}
      </button>
    </div>
    <Overlay @applyEdit="applyEdit" :data="beerToUpdate" v-show="visibleOverlay"></Overlay>
  </div>
</template>

<script>
import axios from "axios"
import Beer from "./components/Beer.vue"
import Overlay from "./components/Overlay.vue"

export default {
  name: "App",
  components: {
    Beer,
    Overlay
  },
  data () {
    return {
      list: [],
      beerToUpdate: {},
      page: 1,
      buttonText: "Show Next",
      visibleOverlay: false,
      visibleShowNext: true
    }
  },
  mounted() {
    axios
      .get("https://api.punkapi.com/v2/beers?page=1&limit=25")
      .then(response => {
        this.list = response.data
      })
  },
  methods: {
    removeBeer(id) {
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
            this.visibleShowNext = false
          }
        });
      this.buttonText = "Show Next"
    },
    startEdit(beer) {
      this.beerToUpdate = beer
      this.visibleOverlay = true
    },
    applyEdit(beer) {
      const index = this.list.findIndex(t => t.id === beer.id);

      if (index === -1) {
        console.error("This beer not found")
        return
      }
      
      this.list[index] = beer
      this.visibleOverlay = false
    }
  }
}
</script>

<style scoped>
.beerlist {
  display: flex;
  flex-wrap: wrap;
  max-width: 1266px;
  margin: auto;
}
@media (max-width: 1290px) {
  .beerlist {
    max-width: 845px;
  }    
}
@media (max-width: 860px) {
  .beerlist {
    max-width: 420px;
  }  
}
.next {
  display: flex;
  justify-content: center;
  margin: 10px 0;  
}
.next__button {
  padding: 5px 10px;
  cursor: pointer;
}
</style>
