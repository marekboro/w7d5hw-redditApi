<template>
  <div id="fullPage">
    <section id="postsAndFavourites">
      <div id="postList">
        <postList :posts="fetchedPosts" />
      </div>
      <div id="favourites">
        <favPosts :posts="favourites" />
      </div>
    </section>
    <section id="filterAndPostDetails">
      <div id="filters">
        <h3>Here will be the filters</h3>
      </div>
      <div id="postDetails">
        <postDetails v-if="selectedPost" :postDetails="selectedPost" />
        <button v-on:click="addToFavourites"> + (fav's)</button>
      </div>
    </section>
  </div>
</template>

<script>
import postList from "@/components/postList";
import favPosts from "@/components/favouritePosts";
import postDetails from "@/components/postDetails";
import { eventBus } from "@/main.js";

export default {
  name: "app",
  data() {
    return {
      pagesToFetch: 2,
      fetchedPosts: [],
      favourites:[],
      selectedPost: null,
      urlStart: "https://old.reddit.com/r/javascript.json?count=25&",
      urlEnd: "before=%22null%22",
    };
  },
  mounted() {
    this.fetchData(this.pagesToFetch);
    eventBus.$on("clicked-post", (post) => (this.selectedPost = post));
  },
  methods: {
    fetchData: function (pagesCount) {
      // takes in a page count
      for (let i = 0; i < pagesCount; i++) {
        fetch(`${this.urlStart}${this.urlEnd}`) // uses a string composition to send fetch request
          .then((promise) => promise.json())
          .then((data) => {
            this.fetchedPosts = this.fetchedPosts.concat(data.data.children); // stores result of fetch instance //! watched
            this.urlEnd = data.data.after; // sets the end of the string
          });
      }
    },
    addToFavourites: function(){
      
      this.selectedPost ? this.favourites.push(this.selectedPost):console.log("cannot add")
    
    },
  },
  components: {
    postList,
    postDetails,
    favPosts
  },
  watch: {
    fetchedPosts: function () {
      console.log("something is happening, but I cannot be more specific");
    },
  },
};
</script>

<style scoped>
#fullPage {
  background-color: darkgreen;
  display: flex;
  flex-direction: row;
  padding: 0%;
  margin: 0%;
}

#postsAndFavourites{
  display: flex;
  flex-direction: column;
  background-color: darkgrey;
  width: 30%;
  /* max-height: 400px; */
  border: rgb(187, 103, 0) solid;
}
#postList{
 background-color: darkorange;
 /* width: 30%; */
 /* position: fixed;
 overflow: auto; */
}
#filterAndPostDetails{
  background-color: lightgoldenrodyellow;
  width: auto;
  width: 70%;
  display: flex;
  flex-direction: column;
  border: rgb(187, 187, 111) solid;
}

#postDetails{
  display: flex;
  flex-direction: row;
}


/* #list {
  height: auto;
  background-color: darkgreen;
  padding: 0%;
  margin: 0%;
} */


/* section{
  padding: 0%;
  margin: 0%;
} */

/* h3{
  padding: 0%;
  margin: 0%;
} */
</style>