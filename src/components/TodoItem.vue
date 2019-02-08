<template>
  <div>
    <p class="todo-item" v-bind:class="{'is-complete':stuff.completed}">
      <input type="checkbox" v-on:change="markComplete">
      {{stuff.title}}
      <button @click="$emit('del-stuff', stuff.id)" class="del"> X </button> 
      <!-- Can see emit event in Vue.js Chrome plugin with passed id as payload-->
    </p>
  </div>
</template>

<script>
export default {
  name: 'oneItem',
  props: ["stuff"],
  methods: {
    markComplete() {
      this.stuff.completed=!this.stuff.completed;
    }
  }
}
</script>

<style scoped>
 .todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }
  .is-complete {
    text-decoration: line-through;
  }
  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
    font-weight: bolder;
    transition:background 0.2s ease-in;
  }

  .del:hover {
    background: #bd0202;
  }
</style>


