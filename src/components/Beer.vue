<template>
  <div class="beer">
    <p class="id">{{ elem.id }}</p>
    <button @click="remove" class="close" title="Delete"><i class="fas fa-times fa-2x"></i></button>
    <div class="image"><img :src="elem.image_url" alt="Beer image"></div>
    <h2 class="name">{{ elem.name }}</h2>
    <p class="description">{{ elem.description }}</p>
    <p class="brewers_tips">{{ elem.brewers_tips }}</p>
    <button @click="edit" class="edit">Edit</button>
  </div>
</template>

<script>

export default {
  name: "Beer",
  props: {
    elem: {
      type: Object,
      required: true
    }
  },
  methods: {
    edit() {
      this.$emit("edit", this.elem)
    },
    remove() {
      this.$emit("remove", this.elem.id)
    }
  }
}
</script>

<style scoped>
.beer {
  position: relative;
  width: 400px;
  border: 1px black solid;
  padding: 5px;
  margin: 5px;
}
.id {
  margin: 0;
  position: absolute;
  left: 20px;
  top: 20px;
}
.edit {
  margin: 5px;
  padding: 5px 10px;
  float: right;
  cursor: pointer;
}
.name {
  margin: 10px 0;
}
.image {
  display: flex;
  justify-content: center;
}
img {
  height: 300px;
}
.close {
  position: absolute;
  right: 20px;
  top: 20px;
  border: 0;
  cursor: pointer;
}
.close:hover {
  color: rgb(60, 60, 60);
}
.description {
  margin: 10px 0;
}
</style>
