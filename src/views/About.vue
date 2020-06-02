<template>
  <div>
    <div class="col-lg-8">
      <div class="video-detail">
        <div class="embed-responsive embed-responsive-16by9">
          <iframe class="embed-responsive-item"
                  :src="videoUrl"
                  allowfullscreen />
        </div>
        <div class="details">
<!--          <h4>{{selectedVideo.snippet.title}}</h4>-->
<!--          <p>{{selectedVideo.snippet.description}}</p>-->
        </div>
      </div>
    </div>
    <VideoList/>
  </div>
</template>

<script>
  import VideoList from "../components/VideoList";

    export default {
        name: "About",
        components:{
            VideoList
        },
        data() {
            return {
                msg:this.$route.query.message
            }
        },
        computed: {
            videoUrl() {
                return `https://www.youtube.com/embed/${this.msg}`
            }
        }
    }
</script>

<style scoped>

</style>