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
      pagesToFetch: 1,
      everythingFetched: [],
      stuffFromAPI: [],
      after: null, // this will need to update once the fist fetch is called.
    };
  },
  mounted() {
    this.fetchData();
    this.everythingFetched.concat(this.stuffFromAPI);
  },
  methods: {
    fetchData() {
      fetch("https://www.reddit.com/r/javascript.json")
        .then((promise) => promise.json())
        .then((data) => (this.stuffFromAPI = data.data.children));
    },
    fetchMultiplePages(){
      for (i=0;i<this.pagesToFetch;i++){
        console.log
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