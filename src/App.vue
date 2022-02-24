<template>
  <post-items :posts="posts" />
  <button @click="loadMorePosts">Read more</button>
</template>

<script>
import PostItems from "./components/post-items.vue";
import { onMounted, ref } from "vue";
export default {
  name: "App",
  components: { PostItems },
  setup() {
    const restOptions = {
      start: 0,
      limit: 6,
    };

    let posts = ref([]);

    const loadMorePosts = async () => {
      const res = await fetch(
        `http://jsonplaceholder.typicode.com/posts?_start=${restOptions.start}&_limit=${restOptions.limit}`
      );
      posts.value = [...posts.value, ...(await res.json())];
      restOptions.start += restOptions.limit;
    };

    onMounted(() => {
      loadMorePosts();
    });

    return {
      posts,
      loadMorePosts,
    };
  },
};
</script>

<style lang="sass">
body
  background-color: aliceblue
  font-size: 62.5%

#app
  max-width: 970px
  margin: auto
</style>
