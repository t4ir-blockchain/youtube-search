<template>
  <div>
    <input class="form-control" v-model="userInput" @keypress.enter="getVideos" type="text">
    <p>{{ $store.state.userInput }}</p>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  name: 'SearchBar',
  data() {
    return {
      userInput: ''
    }
  },
  methods: {
    ...mapActions(['getVideos']),
    
    onInput() {
      // axios 요청을 통해 $store.state.videos


      // App.vue에 $emit을 통해 userInput 전달하는 함수
      this.$emit('onInput', this.userInput)
      // Vuex store에 data를 변경
      // mutations 함수 호출
      this.$store.commit('setUserInput', this.userInput)
      console.log('vuex 스토어 출력:  ' + this.$store.state.userInput)
    }
  }

}
</script>

<style>

</style>