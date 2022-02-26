<template>
  <div class="post">
    <h1 class="post__title">{{ post.title }}</h1>
    <p class="post__body">{{ post.body }}</p>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      default: () => {},
    },
  },
};
</script>

<style lang="sass" >
.post
  text-align: left
  background-color: white
  padding: 1rem
  border-radius: .5rem
  margin: 1rem 0

  &__title
    font-size: 1.8rem

  &__body
    font-size: 1.2rem
</style>