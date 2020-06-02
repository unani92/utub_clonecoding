<template>
  <ul class="list-group col-lg-4">
    <VideoListItem
      v-for="video in videos"
      :key="video.etag"
      @video-select="onVideoSelect"
      :video="video"
    />
  </ul>
</template>

<script>
  import VideoListItem from "./VideoListItem";
    export default {
        name: "VideoList",
        //부모에서 넘겨받은 video 배열을 여기서 정의
        props: {
            videos: Array
        },
        components: {
            VideoListItem,
        },
        methods: {
            onVideoSelect(video) {
                this.$emit('video-select',video)
                this.$router.push({name:'Home',query:{message:video.id.videoId}})
            }
        }
    }
</script>

<style scoped>
  li {
    list-style-type: none;
  }
  iframe {
    width: 500px;
    height: 300px;
  }
  .disabled {
    display: none;
  }
  .videoList {
    border: #2c3e50 1px solid;
    text-align: left;
    width: 500px;
  }
</style>