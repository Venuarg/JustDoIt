<template>
  <div>
    <ul>
      <TodoItem
              v-bind:todo="todo"
              v-for="(todo, i) of todos"
              :key="i"
              v-on:remove="onRemoveItem"
              v-on:toggle="onChangeItem"
      />
    </ul>
  </div>
</template>

<script>
    import TodoItem from '@/components/TodoItem'

    export default {
        props: ['todos'],
        components: {
            TodoItem
        },
        methods: {
            onRemoveItem (id) {
                this.$emit('remove', id)
            },

            onChangeItem (payload) {
                this.$emit('toggle', payload)
            },
        },
    }
</script>

<style scoped>
  ul {
    list-style: none;
    width: 300px;
    margin: 0 auto;
    padding: 0;
  }
</style>