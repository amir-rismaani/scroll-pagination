<template>
  <div class="posts">
    <post-item v-for="post in posts" :key="post.id" :post="post" />
  </div>
</template>

<script>
import PostItem from "./post-item.vue";
export default {
  components: { PostItem },
  props: {
    posts: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style>
</style>