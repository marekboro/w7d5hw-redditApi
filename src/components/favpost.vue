<template>
    <div id="favpostStructure">
        <button v-on:click="handleRemoveClick"> del </button>
         <li v-on:click="handlePostClick">{{post.data.title.slice(0,28)+ " ... "+ post.data.title.slice(-10)}}</li>
    </div>

  
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

        },
        handleRemoveClick: function(){
        eventBus.$emit('post-to-delete-from-favs', this.post)
        console.log("trying to del")
        }
    }

}
</script>

<style scoped>

#favpostStructure{
    display: flex;
    flex-flow: row;
}

#favpostStructure>li{
    list-style: none;
}
/* div{
    display: flex;
    flex-flow: row;
    display: flex;
    justify-content: space-between;
    
}
li{
    background-color: antiquewhite;
    height:20%;
    list-style: none;
    margin: 2px;
    padding: 2px;
    border: solid 2px;
}
li:hover{
    background-color: rgb(250, 216, 173);
    cursor: pointer;
} */

</style>