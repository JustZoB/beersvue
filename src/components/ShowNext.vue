<template>
    <div class="next__wrap">
        <button @click="$emit('next')" class="next">{{ buttonText }}</button>
    </div>
</template>

<script>

export default {
  name: "ShowNext",
  props: ['buttonText'],
  methods: {
    deleteBeer(id) {
        this.$emit('deleteBeer', id)
    }
  }
}
</script>

<style scoped>
.next__wrap {
    display: flex;
    justify-content: center;
    margin: 10px 0;  
}
.next {
    padding: 5px 10px;
    cursor: pointer;
}
</style>
