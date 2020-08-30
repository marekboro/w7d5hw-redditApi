<template>
  <div>
    <h3>{{postDetails.data.title}}</h3>
    <!-- <img :src="`${this.imaggelink}`" width="400" alt="stuf"> -->
        <div v-if="imagelink">
        <img :src="`${this.imagelink}`" width="400" alt="stuf">
        </div>
        <!-- <div v-if="imagelink"> -->
            <!-- <img :src="`${this.imageLink}`" width="400" alt="stuf"> -->
            <!-- <h3>Image</h3> -->
        <!-- </div> -->
        <div v-if="videoLink">
            <video :src="`${this.videoLink}`" width="400" alt="stuf" controls/>
                <h3>Video</h3>
        </div>
    <!-- <h3>{{postDetails.data.permalink}}</h3> -->
    <!-- <img :src="`${urltoLoad2}.jpg`" alt="stuf"> -->
    <!-- <img :src="`https://i.redd.it/g57163jx3yj51.jpg`" width="200" alt="stuf"> -->
    <!-- <h3>{{getLink()}}</h3> -->
    <!-- <h3>{{postDetails.data.url}}</h3> -->
    <!-- <p>{{this.postcontent}}</p> -->
  </div>
</template>

<script>
export default {
  name: "post-detail",
  props: ["postDetails"],
  data() {
    return {
      postcontent: [],
    //   urlToLoad:"",
      urltoLoad2: this.postDetails.data.url,
      postHint: null,
    //   imagelink:null,
    //   videoLink:null,
    //   finalLink:null,
      imagelink:"",
      videoLink:"",
      finalLink:"",
    //   image1: this.postDetails.data.url_overridden_by_dest,
      permalink: this.postDetails.data.permalink,
    //   urltoLoad3: `https.www${permalink}`,
      
    };
  },
  mounted() {
    this.fetchPostDetails();
    this.decideOnMediaLink();
    this.getLink();
    // console.log("content Fetched")
    // console.log("toittle:"+this.urltoLoad2)
  },
  computed: {
      
       
  },
  methods: {
    getLink: function(){
        let a = "https://www.reddit.com"
        let b = this.postDetails.data.permalink.slice(0,-1);
        let c = ".json";
        return a+b+c
        
      },
    fetchPostDetails: function () {
        this.imagelink="";
        this.videoLink="";
        this.finalLink="";

      fetch(`${this.getLink()}`)
        .then((promise) => promise.json())
        //// .then((data) => (this.postcontent = data[0].data.children.data.selftext));
        .then((data) => {
            this.postcontent = data[0].data.children[0].data.title;
            this.postHint = data[0].data.children[0].data.post_hint;
            console.log("post hint:" +this.postHint)
            // this.imagelink = data[0].data.children[0].data.url_overridden_by_dest;
            // this.videoLink = data[0].data.children[0].data.media.reddit_video.fallback_url;
            // this.videoLink = data[0].data.children[0].media.reddit_video.fallback_url;
            // console.log(this.imagelink);
            console.log(this.videoLink);

           
           // this.postHint === "image" ? this.finalLink = data[0].data.children[0].data.url_overridden_by_dest : this.finalLink = data[0].data.children[0].media.reddit_video.fallback_url
           
           this.postHint === "image" ? this.imagelink = data[0].data.children[0].data.url_overridden_by_dest 
            : this.postHint === "hosted:video" ? this.videoLink = data[0].data.children[0].data.media.reddit_video.fallback_url : console.log("neither image nor video")
            


            });
    },
    decideOnMediaLink: async function(){
        if (this.postHint = "image"){
            this.finalLink = this.imagelink;
        }
        if (this.postHint = "hosted:video"){
            this.finalLink = this.videoLink;
        }
        
        // this.postHint = "image" ? 
        
    }
  },
  watch:{
      postDetails: function(){
        // console.log("post Details Changed")
        // console.log("current title:"+this.postDetails.data.title)
        // console.log("urltoLoad2:"+this.urltoLoad2)
        // this.getLink();
        // urltoLoad2 = this.postDetails.data.url
        // console.log("postDetails.url2"+this.postDetails.url)
        // this.urlToLoad = postDetails.url;
        this.fetchPostDetails();
        // this.decideOnMediaLink();

      },
      postHint: function(){
          this.decideOnMediaLink();
      }
  }
};
</script>

<style>
</style>