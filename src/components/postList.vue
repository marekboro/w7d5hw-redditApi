<template>
  <div>
      <h3>Posts:</h3>
      <ul>
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

</style>