<template>
    <!-- Main Content -->
  <div class="container">
    <div class="row">
      <div class="col-lg-8 col-md-10 mx-auto">
        <PostList    v-for="blog in blogs"
                     :key="blog.name"
                     :blog="blog"></PostList>
        <!-- Pager -->
        <div class="clearfix">
          <a class="btn btn-primary float-right" href="#">Older Posts &rarr;</a>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import PostList from "~/components/PostList.vue"

export default {
  components: {
    'PostList': PostList
  },
  props: {
    blogs: {
      type: Array
    }
  }
}

</script>
