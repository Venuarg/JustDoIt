<template>
  <li>
    <div>
      <CommonButton
          v-on:click="onCompleted(todo.id, !todo.completed)"
          type="success">
        <font-awesome-icon icon="fa-solid fa-check"/>
      </CommonButton>
    </div>

    <div class="title">
      <span v-bind:class="{done: todo.completed}">
        {{ todo.title }}
      </span>
    </div>

    <div>
      <CommonButton
          v-on:click="$emit('remove', todo.id)"
          type="danger">
        <font-awesome-icon icon="fa-solid fa-trash"/>
      </CommonButton>
    </div>
  </li>
</template>

<script>
import CommonButton from "@/components/CommonButton";

export default {
  components: {
    CommonButton
  },

  props: {
    todo: {
      type: Object,
      required: true
    },
  },

  methods: {
    onCompleted(id, value) {
      this.$emit('toggle', {
        id,
        value
      })
    }
  },
}
</script>

<style scoped>
li {
    height: 36px;
    border: none;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 4px;
    margin-bottom: 16px;
    color: #808080;
    background: hsl(196, 17%, 17%);
    border-radius: 18px;
}

.title {
    text-align: left;
    flex: 1;
    padding: 0 12px;
}

input {
    margin-right: 1rem;
}

.done {
    text-decoration: line-through;
}
</style>