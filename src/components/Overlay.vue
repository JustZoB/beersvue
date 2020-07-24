<template>
  <div id="overlay">
    <div id="modal">
      <textarea rows="1" cols="45" class="textarea_name" v-model="dataValue.name"></textarea>
      <textarea rows="10" cols="45" class="textarea_description" v-model="dataValue.description"></textarea>
      <button @click="applyEdit" class="applyEdit">Apply edit</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Overlay",
  props: {
    data: {
      type: Object
    }
  },
  data() {
    return {
      dataValue: {}
    }
  },
  watch: {
    data(data) {
      this.dataValue = { ...data }
    }
  },
  methods: {
    applyEdit() {
      this.$emit("applyEdit", this.dataValue);
    }
  }
}
</script>

<style scoped>
#overlay {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  box-sizing: content-box;
  background-color: rgba(0, 0, 0, 0.5);
}
#modal {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  position: absolute;
  background-color: white;
  transform: translate(-50%, -50%);
  left: 50%;
  top: 50%;
  width: 500px;
  height: 500px;
}
.textarea_name {
  font-size: 16px;
  width: 400px;
  height: 50px;
  padding: 3px;
  resize: none;
  margin-bottom: 10px;
}
.textarea_description {
  font-size: 16px;
  width: 400px;
  padding: 3px;
  height: 300px;
  resize: none;
}
.applyEdit {
  padding: 5px 10px;
  margin: 10px;
}
</style>
