<template>
  <div>
    <input class="form-control" v-model="userInput" @keypress.enter="onInput" type="text">
  </div>
</template>

<script>

export default {
  name: 'SearchBar',
  data() {
    return {
      userInput: ''
    }
  },
  methods: {
    onInput() {
      // App.vue에 $emit을 통해 userInput 전달하는 함수
      this.$emit('onInput', this.userInput)
    }
  }

}
</script>

<style>

</style>