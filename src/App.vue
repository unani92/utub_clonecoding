<template>
  <div id="app">
    <div class="container">
<!--2. 자식의 요청을 듣고 콜백을 실행한다.-->
      <SearchBar @input-change="onInputChange" />
<!-- 1. 데이터를 가진 부모가 자식에게 던질 준비를 한다.     -->
<!-- 단방향 바인딩을 통해 videos 데이터를 videos라는 이름으로 VideoList에 넘겨준다.-->
      <div class="row">
        <videoDetail :selectedVideo="selectedVideo" />
        <VideoList @video-select="onVideoSelect" :videos="videos" :q="q" />
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios'
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";

const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'App',
  components: {
      SearchBar,
      VideoList,
      VideoDetail
  },
  data(){
      return {
          inputValue: '',
          videos: [],
          selectedVideo: null,
      }
  },
  methods: {
      onInputChange(inputText) {
          this.inputValue = inputText
          // emit에서 온 데이터를 수정까지 완료
          axios.get(API_URL, {
              params: {
                  key: API_KEY,
                  part: "snippet",
                  type: "video",
                  q: this.inputValue,
              }
          })
            .then(response => {
                response.data.items.forEach(item => {
                    const parser = new DOMParser()
                    const doc = parser.parseFromString(item.snippet.title, 'text/html')
                    item.snippet.title = doc.body.innerText
                })
                this.videos = response.data.items
            })
            .catch(error => alert(error))
      },
      onVideoSelect(video) {
          this.selectedVideo = video
      }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
