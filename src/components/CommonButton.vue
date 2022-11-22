<template>
  <div :class='computedClass'> <!-- : сокращение для v-bind: -->
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "CommonButton",
  props: {
    type: String // принимает success и danger
  },
  computed: {
    computedClass () {
      return {
        btn: true,
        btn__success: this.type === 'success',
        btn__danger: this.type === 'danger'
      }
    }
  }
}
</script>

<style scoped>

.btn {
    display: flex;
    justify-content: center;
    align-items: center;
    color: #2c3e50;
    width: 28px;
    height: 28px;
    cursor: pointer;
    background: #949EA4FF;
    border-radius: 14px;

    transition: background .2s;
}

.btn__success:hover {
    background: seagreen;
}

.btn__danger:hover {
    background: indianred;
}

</style>