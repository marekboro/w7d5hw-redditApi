<template>
  <div>
    <h3>Favourites</h3>
    <li>
    
    <singlePost v-for="(post,index) in posts" :key="index" :post="post" />
    </li>
  </div>
</template>

<script>
import singlePost from "@/components/favpost.vue";
export default {
  name: "favPosts",
  props: ["posts"],
  methods: {
      
  },
  components: {
    singlePost,
  },
};
</script>

<style>
h3{
    text-align: center;
}
li{
list-style: none;}
</style>