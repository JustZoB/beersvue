<template>
  <div class='beerlist'>
    <Beer 
        v-for="elem of list" 
        :key="elem.id"
        :elem="elem"
        @delete="deleteBeer"
    />
  </div>
</template>

<script>
import Beer from './Beer.vue'

export default {
  name: "BeerList",
  props: ['list'],
  components: {
    Beer
  },
  methods: {
    deleteBeer(id) {
        this.$emit('deleteBeer', id)
    },
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
</style>
