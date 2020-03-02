<template>
  <div>
    <!-- 블로그 Navigation   -->
    <BlogNavigation></BlogNavigation>
    <nuxt />
  </div>

</template>

<script>
  import BlogNavigation from "~/components/BlogNavigation.vue"
export default {
  components: {
    'BlogNavigation': BlogNavigation

  },
}
</script>

<style>

</style>
