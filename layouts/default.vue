<template>
  <div>
  <!-- 블로그 Navigation   -->
  <BlogNavigation></BlogNavigation>

  <!-- 블로그 header -->
  <BlogHeader></BlogHeader>
  
  <!-- 블로그 메인 content -->
  <BlogMainContent></BlogMainContent>
  
  <hr>
  
  <!-- 블로그 footer -->
  <BlogFooter></BlogFooter>
  </div>
 
</template>

<script>
import BlogNavigation from "~/components/BlogNavigation.vue"
import BlogHeader from "~/components/BlogHeader.vue"
import BlogMainContent from "~/components/BlogMainContent.vue"
import BlogFooter from "~/components/BlogFooter.vue"

export default {
  components: {
    'BlogNavigation': BlogNavigation,
    'BlogHeader': BlogHeader,
    'BlogMainContent': BlogMainContent,
    'BlogFooter': BlogFooter
  }
}
</script>

<style>

</style>
