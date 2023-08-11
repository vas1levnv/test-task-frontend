<script>
export default {
  name: "user-item",
  props: {
    item: {
      type: Object,
      required: true
    }
  }
}
</script>

<template>
  <div class="item" @click="$emit('add', item)">{{ item.name }}</div>
</template>

<style scoped>
.item {
  padding: 20px;
  border: 5px solid black;
}

</style>