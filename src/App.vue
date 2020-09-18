<template>
  <div class="main-container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
      <VideoDetail class="col-sm-8" :video="selectedVideo"></VideoDetail>
      <VideoList class="col-sm-4" :videos="videos" @videoSelect="onVideoSelect"></VideoList>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";

const Api_key = "AIzaSyBNS1VyZbYQejS7ULIsREDAlnSJ519O6WU";

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },

  data() {
    return {
      videos: [],
      selectedVideo: null
    };
  },

  methods: {
    onTermChange(searchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: Api_key,
            type: "video",
            part: "snippet",
            q: searchTerm
          }
        })
        .then(response => {
          this.videos = response.data.items;
        });
    },

    onVideoSelect(video) {
      this.selectedVideo = video;
    }
  }
};
</script>


<style scoped>
.main-container {
  width: 80%;
  margin-left: auto;
  margin-right: auto;
}
</style>