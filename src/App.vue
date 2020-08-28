<template>
  <div>
    <h3>This is a test of the VUE</h3>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {

      pagesToFetch: 2,
      everythingFetched: [],
      stuffFromAPI: [],
      after: "before=%22null%22", // this will need to update once the fist fetch is called.
      // currentUrl = "https://www.reddit.com/r/javascript.json" + this.after,
      startPage: "https://old.reddit.com/r/javascript/?count=25&before=%22null%22",
      startPage1: "https://old.reddit.com/r/javascript.json?count=25&before=%22null%22",
      nextPage: "https://old.reddit.com/r/javascript/?count=25&after=t3_igr2c6",
      nextPage1: "https://old.reddit.com/r/javascript.json?count=25&after=t3_igr2c6",
      urlStart: "https://old.reddit.com/r/javascript.json?count=25&",
      urlEnd: "before=%22null%22"


    };
  },
  mounted() {
    this.fetchMultiplePages(this.pagesToFetch);
    // this.fetchData();
    // this.fetchMultiplePages(this.pagesToFetch);
    // this.everythingFetched.concat(this.stuffFromAPI);
  },
  methods: {
    fetchData() {
      // fetch("https://www.reddit.com/r/javascript.json")
  
      // console.log(`dupa`)
      // console.log(`https://old.reddit.com/r/javascript.jsaon?count=25&before=null%`)
      // fetch(`${this.startPage1}`)
      fetch(`${this.urlStart}${this.urlEnd}`)
        .then((promise) => promise.json())
        .then((data) => {
          this.stuffFromAPI = data.data.children;
          this.after = data.data.after;
        });
    },

    fetchMultiplePages: function(pagesCount){
      
      for(let i = 0; i<pagesCount; i++){
        console.log("page:");
        fetch(`${this.urlStart}${this.urlEnd}`)
        .then((promise) => promise.json())
        .then((data) => {
          this.stuffFromAPI = data.data.children;
          this.urlEnd = data.data.after;
        });

      }
    },
    mergeFetchOntoDatabase() {
      this.everythingFetched = this.everythingFetched.concat(this.stuffFromAPI);
    },
  },
  watch: {
    stuffFromAPI: function () {
      this.mergeFetchOntoDatabase();
    },
  },
};
</script>

<style>
</style>