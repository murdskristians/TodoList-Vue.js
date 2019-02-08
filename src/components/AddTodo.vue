<template>
  <dir>
    <form @submit="addTodo">
      <input type="text" v-model="title" name="title" placeholder="Add Todo...">
      <input type="submit" value="Submit" class="btn">
    </form>
  </dir>
</template>

<script>
//Dont need next line because axios can handle ids
// import uuid from 'uuid';

export default {
  name: "AddTodo",
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addTodo(e) {
      //Prevents default submision to file so we can emit
      e.preventDefault();

      if (this.title == '') return;

      const newTodo ={
        //Dont need next line because axios can handle ids
        // id: uuid.v4(),
        title: this.title,
        completed: false
      }
      //Send up to parrent (App.vue)
      this.$emit('add-todo', newTodo);
      this.title='';
    }
  }
}
</script>

<style scoped>
  form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
  }
</style>
