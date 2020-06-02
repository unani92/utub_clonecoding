<template>
  <li @click="onVideoSelect" class="video-list-item list-group-item">
    <img :src="thumbnailUrl" alt="youtube-thumbnail">
    <div class="media-body">
      <span v-html="video.snippet.title"/>
    </div>
  </li>
</template>

<script>
    export default {
        name: "VideoListItem",
        props: {
            video: Object
        },
        methods:{
            onVideoSelect() {
                this.$emit('video-select',this.video)

            }
        },
        computed: {
            thumbnailUrl() {
                return this.video.snippet.thumbnails.default.url
            }
        }
    }
</script>

<style scoped>
  .video-list-item {
    display: flex;
    cursor: pointer;
  }
  .video-list-item:hover {
    background: blanchedalmond;
  }
  .media-body {
    margin: auto 0;
    text-align: left;
    padding-left: 10px;
  }
</style>