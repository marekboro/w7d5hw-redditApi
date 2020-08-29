<template>
    <div>
  <li v-on:click="handlePostClick">{{post.data.title}}</li>
  <li>Comments: {{post.data.num_comments}}</li>
  <!-- <li>{{post.data.selftext_html}}</li> -->
  </div>
  <!-- <li>Hello</li> -->
  
</template>

<script>
import {eventBus} from '@/main.js';

export default {
    name: 'postView',
    props:['post'],
    methods: {
        handlePostClick(){
            eventBus.$emit('clicked-post', this.post);
            console.log(`clicked ${this.post.data.title}`);

        }
    }

}
</script>

<style>

</style>