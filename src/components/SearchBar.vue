<template>
  <div>
    <input v-model="userInput" @keypress.enter="input" type="text">
    
    <div v-if="results.length > 0">
      <iframe :src="`https://www.youtube.com/embed/${results[0].id.videoId}`"></iframe>
    </div>

    <ul>
      <li v-for="result in results" :key="result.id.videoId">
        {{ result.snippet.title }}
        <img :src="result.snippet.thumbnails.default.url">
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'SearchBar',
  data() {
    return {
      userInput: '',
      results: []
    }
  },
  methods: {
    input() {
      // 1. 입력된 검색어를 가지고,
      const baseURL = 'https://www.googleapis.com/youtube/v3/search'
      const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY

      // 2. Youtube API에 요청을 보내어
      axios.get(baseURL, {
        params: {
          // key, part, q
          key: API_KEY,
          part: 'snippet',
          type: 'video',
          q: this.userInput,
          maxResults: 10
        }
      })
        .then(response => {
          console.log(response.data.items)
          this.results = response.data.items
        })
      // 3. 검색어로 검색한 결과를 가져옴
      console.log('검색어 입력 되었음')
    }
  }

}
</script>

<style>

</style>