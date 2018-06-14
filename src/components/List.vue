<template>
    <div>
       <div v-for="post in posts" :key="post.id">
        <p>Author: {{post.author}}</p>
        <p>Created at: {{post.timeStamp}}</p>
        <button @click="removePost(post.id)">Remove</button>
        <p>{{post.content}}</p>
      </div>
    </div>
</template>

<script>
export default {
  props: ["posts", "removePost"]
};
</script>
<style scoped>
</style>

