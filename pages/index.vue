<template>
  <div>
    <!-- 블로그 Navigation   -->
    <BlogNavigation></BlogNavigation>
    <!-- 블로그 header -->
    <BlogHeader></BlogHeader>
    <!-- 블로그 메인 content -->
    <BlogMainContent :blogs="blogs"></BlogMainContent>
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
  import blogsEn from '~/contents/en/blogsEn.js'
  import blogsEs from '~/contents/es/blogsEs.js'


export default {
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
    'BlogFooter': BlogFooter},

  transition: {
    name: 'slide-fade'
  },

  head () {
    return {
      title: 'YEEUN Devlog',
      // htmlAttrs: {
      //   lang: this.$i18n.locale,
      // },
      // script: [{ src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' }],
      // meta: [
      //   { name: "author", content: "Marina Aisa" },
      //   { name: "description", property: "og:description", content: this.$t('indexPageHead.description'), hid: "description" },
      //   { property: "og:title", content: this.$t('indexPageHead.title') },
      //   { property: "og:image", content: this.ogImage },
      //   { name: "twitter:description", content: this.$t('indexPageHead.description') },
      //   { name: "twitter:image", content: this.ogImage }
      // ]
    };
  },

  computed: {
    ogImage: function () {
      return;
    }
  }
}
</script>

<style>

</style>
