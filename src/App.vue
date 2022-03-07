<template>
  <div id="infinite-posts">
    <post-items :posts="posts" />
  </div>
  <!-- <button v-if="hasPosts" @click="loadMorePosts">Load more</button> -->
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
    let hasPosts = ref([true]);
    let latestPosts = [];
    const loadMorePosts = async () => {
      const res = await fetch(
        `http://jsonplaceholder.typicode.com/posts?_start=${restOptions.start}&_limit=${restOptions.limit}`
      );
      latestPosts = await res.json();
      if (latestPosts.length) {
        posts.value = [...posts.value, ...latestPosts];
        restOptions.start += restOptions.limit;
      } else {
        hasPosts.value = false;
      }
    };

    window.addEventListener("scroll", () => {
      let bottomOfWindow =
        document.documentElement.scrollTop + window.innerHeight ===
        document.documentElement.offsetHeight;
      if (hasPosts.value && bottomOfWindow) {
        loadMorePosts();
      }
    });

    onMounted(() => {
      const infinitePostsElem = document.querySelector("#infinite-posts");
      infinitePostsElem.addEventListener("scroll", () => {
        if (
          infinitePostsElem.scrollTop + infinitePostsElem.clientHeight >=
          infinitePostsElem.scrollHeight
        ) {
          loadMorePosts();
        }
      });
      loadMorePosts();
    });

    return {
      posts,
      loadMorePosts,
      hasPosts,
    };
  },
};
</script>

<style lang="sass">
body
  background-color: #00000009
  font-size: 62.5%

#app
  max-width: 970px
  margin: auto
</style>
