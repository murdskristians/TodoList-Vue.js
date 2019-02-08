<template>
  <div>
    <div :key="element.id" v-for="element in impTD">
      <!-- Can see emit event in Vue.js Chrome plugin with passed id as payload-->
      <Item :stuff="element" v-on:del-stuff="$emit('del-stuff', element.id)"/>
    </div>
  </div>
</template>

<script>
import Item from './TodoItem.vue'

export default {
  name: 'Loop',
  components: {
    Item
  },
  props: ["impTD"]
}
</script>

