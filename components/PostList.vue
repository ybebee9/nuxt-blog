<template>
  <div>
    <nuxt-link
      :to="localePath({ name: 'blog-slug', params: { slug: blog.name }})"
    >
    <div class="post-preview">
      <a href="post.html">
        <h2 class="post-title">
          {{ blog.title }}
        </h2>
        <h3 class="post-subtitle">
          {{ blog.description }}
        </h3>
      </a>
      <p class="post-meta">Posted by
        <a href="#">Start Bootstrap</a>
        on September 24, 2019</p>
    </div>
    </nuxt-link>
    <hr>

  </div>
</template>

<script>
    export default {
      name: "PostList",
      props: {
        blog: {
          type: Object
        }
      }
    }
</script>

<style scoped>

</style>
