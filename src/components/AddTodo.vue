<template>
  <div class="createWrapper">
    <input type="text" v-model="title" placeholder="Add a task..." @keyup.enter="onSubmit">
    <button @click="onSubmit">I Got This!</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title: ''
    }
  },

  methods: {
    onSubmit () {
      if (this.title.trim()) {
        this.$emit('add-todo', this.title)
        this.title = ''
      }
    }
  }
}
</script>

<style scoped>
.createWrapper {
    margin: 0 auto 40px;
    height: 30px;
    display: flex;
    width: 500px;
    border-radius: 12px;
    overflow: hidden;
}

input {
    flex: 1;
    background: hsl(180, 4%, 10%);
    border: none;
    color: #fff;
    padding-left: 12px;
}

button {
    border: none;
    cursor: pointer;
    padding: 0 8px;
    background: hsl(8, 60%, 92%);
}

</style>
