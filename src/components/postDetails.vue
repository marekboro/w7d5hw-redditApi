<template>
  <div>
    <h3>{{postDetails.data.title}}</h3>
    <div v-if="imageLink">
      <img :src="`${this.imageLink}`" width="400" alt="stuf" />
    </div>
    <div v-if="videoLink">
      <video :src="`${this.videoLink}`" width="400" alt="stuf" controls />
    </div>
  </div>
</template>

<script>
export default {
  name: "post-detail",
  props: ["postDetails"],
  data() {
    return {
      postcontent: [],
      urltoLoad2: this.postDetails.data.url,
      postHint: null,
      imageLink: "",
      videoLink: "",
      finalLink: "",
      permalink: this.postDetails.data.permalink,
    };
  },
  mounted() {
    this.fetchPostDetails();
    this.getLink();
  },
  computed: {},
  methods: {
    getLink: function () {
      let a = "https://www.reddit.com";
      let b = this.postDetails.data.permalink.slice(0, -1);
      let c = ".json";
      return a + b + c;
    },
    fetchPostDetails: function () {
      this.imageLink = "";
      this.videoLink = "";
      this.linkedLink = "";

      fetch(`${this.getLink()}`)
        .then((promise) => promise.json())
        //// .then((data) => (this.postcontent = data[0].data.children.data.selftext));
        .then((data) => {
          this.postcontent = data[0].data.children[0].data.title;
          this.postHint = data[0].data.children[0].data.post_hint;
          
          
          //https://i.imgur.com/P9QWwtV.jpg"
        //   this.postHint === "image" || "link"
        //     ? (this.imageLink =
        //         data[0].data.children[0].data.url_overridden_by_dest)
        //     : this.postHint === "hosted:video"
        //     ? (this.videoLink =
        //         data[0].data.children[0].data.media.reddit_video.fallback_url)
        //     : console.log("neither image nor video");
          this.postHint === "image" // || "link"
            ? (this.imageLink =
                data[0].data.children[0].data.url_overridden_by_dest)
            : this.postHint === "link" 
            ? (this.imageLink = 
                data[0].data.children[0].data.url_overridden_by_dest+".jpg") :
            
            
            this.postHint === "hosted:video"
            ? (this.videoLink =
                data[0].data.children[0].data.media.reddit_video.fallback_url)
            : console.log("neither image nor video");
        });
    },
  },
  watch: {
    postDetails: function () {
      this.fetchPostDetails();
    },
    postHint: function () {
      this.decideOnMediaLink();
    },
  },
};
</script>

<style>
</style>