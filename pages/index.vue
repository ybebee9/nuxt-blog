<template>
  <div>
    <client-only>
    <!-- 블로그 Navigation   -->
    <BlogNavigation></BlogNavigation>
    <!-- 블로그 header -->
    <BlogHeader></BlogHeader>
    <!-- 블로그 메인 content -->
    <BlogMainContent :blogs="blogs"></BlogMainContent>


    <!-- 블로그 footer -->
    <BlogFooter></BlogFooter>
    </client-only>
  </div>

</template>

<script>
  import BlogNavigation from "~/components/BlogNavigation.vue"
  import BlogHeader from "~/components/BlogHeader.vue"
  import BlogMainContent from "~/components/BlogMainContent.vue"
  import BlogFooter from "~/components/BlogFooter.vue"
  import blogsEn from '~/contents/en/blogsEn.js'
  import blogsEs from '~/contents/es/blogsEs.js'

export default {

  name: 'Index',
  async asyncData ({app}) {

    const blogs = app.i18n.locale === 'en' ? blogsEn : blogsEs

    async function asyncImport (blogName) {
      const wholeMD = await import(`~/contents/blog/${blogName}.md`)
      return wholeMD.attributes
    }

    return Promise.all(blogs.map(blog => asyncImport(blog)))
      .then((res) => {
        return {
          blogs: res
        }
      })
  },

  components: {
    'BlogNavigation': BlogNavigation,
    'BlogHeader': BlogHeader,
    'BlogMainContent': BlogMainContent,
    'BlogFooter': BlogFooter
  },

  head () {
    return {
      title: 'YEEUN Devlog'
    };
  }
}
</script>

<style>

</style>
