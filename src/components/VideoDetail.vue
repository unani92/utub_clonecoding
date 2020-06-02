<template>
  <div class="col-lg-8">
    <div class="video-detail">
      <div class="embed-responsive embed-responsive-16by9">
        <iframe class="embed-responsive-item"
                :src="videoUrl"
                allowfullscreen />
      </div>
      <div class="details">
<!--        <h4>{{selectedVideo.snippet.title}}</h4>-->
<!--        <p>{{selectedVideo.snippet.description}}</p>-->
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: "VideoDetail",
        props: {
            selectedVideo: Object,
        },
        computed: {
            videoUrl() {
                return `https://www.youtube.com/embed/${this.$route.query.message}`
                // this.selectedVideo.id.videoId
            }
        }
    }
</script>

<style scoped>
  .video-detail {
    margin-top: 10px;
    padding: 10px;
    border: 1px solid #dddddd;
    border-radius: 5px;
  }
</style>