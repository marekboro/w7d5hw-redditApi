<template>
  <div>
      <h3>Posts loaded: {{posts.length}}</h3>
      <ul class="postViewer">
          <li>
              <singlePost v-for="(post,index) in posts" :key="index" :post="post" />
          </li>
      </ul>

  </div>
</template>

<script>

import singlePost from '@/components/post.vue'
export default {
    name: 'post-list',
    props: ['posts'],
    components: {
        singlePost
    }

}
</script>

<style>
h3{
    text-align: center;
    padding: 0%;
    margin: 0%;
}
ul{
    list-style: none;
}
/* div{
    background-color: cyan;
}


.postViewer{
    max-height: 500px;
    background: darkgoldenrod;
    position: fixed;
    overflow: auto;
} */

</style>