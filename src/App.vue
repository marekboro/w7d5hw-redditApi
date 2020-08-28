<template>
  <div>
    <h3>This is a test of the VUE</h3>
    <postList :posts="fetchedPosts"/>
  </div>
</template>

<script>
import postList from '@/components/postList'

export default {
  name: "app",
  data() {
    return {

      pagesToFetch: 2,
      fetchedPosts: [],
      urlStart: "https://old.reddit.com/r/javascript.json?count=25&",
      urlEnd: "before=%22null%22"
    };
  },
  mounted() {
    this.fetchData(this.pagesToFetch);
   
  },
  methods: {
    fetchData: function(pagesCount){              // takes in a page count 
      for(let i = 0; i<pagesCount; i++){
        fetch(`${this.urlStart}${this.urlEnd}`)   // uses a string composition to send fetch request
        .then((promise) => promise.json())
        .then((data) => 
              {
              this.fetchedPosts = this.fetchedPosts.concat(data.data.children); // stores result of fetch instance //! watched
              this.urlEnd = data.data.after;          // sets the end of the string 
              });
      }
    },
    
  },
  components:{
    postList
  },
  watch: {
    fetchedPosts: function () {
      console.log("something is happening, but I cannot be more specific")        
    },
  },
};
</script>

<style>
</style>