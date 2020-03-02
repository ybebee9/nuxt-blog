<template>
  <div class="blogSelected">
    <div class="intro">
      <div class="elevate-cover">
        <div class="elevate-cover__titleH1">
          <h1 >
            {{ title }}
          </h1>
          <span class="blogSelected-year">{{ year }}</span>
        </div>
        <p class="elevate-cover__description">{{ description }}</p>
      </div>
    </div>
    <div class="container small">
      <client-only>
        <DynamicMarkdown
          :render-func="renderFunc"
          :static-render-funcs="staticRenderFuncs"
          :extra-component="extraComponent" />
      </client-only>
    </div>
  </div>
</template>

<script lang="js">

  import DynamicMarkdown from "~/components/Markdown/DynamicMarkdown.vue"


  export default {

    async asyncData ({params, app}) {
      const fileContent = await import(`~/contents/blog/${params.slug}.md`)
      const attr = fileContent.attributes
      return {
        name: params.slug,
        title: attr.title,
        trans: attr.trans,
        year: attr.year,
        id: attr.id,
        cardAlt: attr.cardAlt,
        noMainImage: attr.noMainImage,
        description: attr.description,
        extraComponent: attr.extraComponent,
        renderFunc: `(${fileContent.vue.render})`,
        staticRenderFuncs: `[${fileContent.vue.staticRenderFns}]`
        // image: {
        //   main: attr.image && attr.image.main,
        //   og: attr.image && attr.image.og
        // }
      }
    },

    // nuxtI18n: {
    //   seo: false
    // },

    components: { DynamicMarkdown},

    head () {
      return {
        title: this.pageTitle
        // htmlAttrs: {
        //   lang: this.$i18n.locale,
        // },
        // meta: [
        //   { name: "author", content: "Marina Aisa" },
        //   { name: "description", property: "og:description", content: this.description, hid: "description" },
        //   { property: "og:title", content: this.pageTitle },
        //   { property: "og:image", content: this.ogImage },
        //   { name: "twitter:description", content: this.description },
        //   { name: "twitter:image", content: this.ogImage }
        // ],
        // link: [
        //   this.hreflang
        // ]
      };
    },

    transition: {
      name: 'slide-fade'
    },

    computed: {
      // ogImage () {
      //   return `${process.env.baseUrl}/images/blog/${this.id}/_thumbnail.jpg`;
      // },
      pageTitle () {
        return this.title + ' – ybebee9';
      },
      // showLocales () {
      //   return this.$i18n.locales.filter(locale => locale.code !== this.$i18n.locale)
      // },
      // hreflang () {
      //   if (!this.trans) {
      //     return ''
      //   }
      //   return {
      //     hid: 'alternate-hreflang-' + this.showLocales[0].iso,
      //     rel: 'alternate',
      //     href: `${process.env.baseUrl + (this.showLocales[0].code === 'en' ? '' : '/es')}/blog/${this.trans}`,
      //     hreflang: this.showLocales[0].code
      //   }
      // },

      extraComponentLoader () {
        if (!this.extraComponent) {
          return null
        }
        return () => import(`~/components/blog/${this.extraComponent}.vue`)
      }
    }
  }
</script>

<style lang="scss">
.overflowhidden {
  overflow: hidden;
}
.blogSelected-horizontalImage {

  height: 56rem;
  background-size: contain;
  transition: all ease .35s;
  opacity: 0;

  &[lazy='loading'] {
    filter: blur(15px);
    background-repeat: no-repeat!important;
    background-size: contain!important;
  }
  &[lazy='loaded'] {
    opacity: 1;
    background-repeat: no-repeat!important;
    background-size: contain!important;
  }
  .intro {
    display: flex;
  }
}
.elevate-cover {
  display: flex;
  flex-direction: column;
  min-height: 325px;
  padding-top: 100px;


  &__img, &__textOffset {
    width: 100%;
  }

  &__left {
    width: 100%;
    padding: 2.4rem;
    margin-bottom: auto;


  }

  &__textOffset {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  &__title {
    font-size: 3rem;
    font-family: 'Tiempos Headline', Arial, sans-serif;
  }

  &__description {
    margin: 0;
    opacity: 0;
    animation: fadeinmove .5s ease;
    animation-delay: .5s;
    animation-fill-mode: forwards;
  }
  &__titleH1 {
    max-width: 1100px;
    text-align: center;
    padding-right: 15px;
    padding-left: 15px;
    margin-right: auto;
    margin-left: auto;
  }
}
.dynamicMarkdown {
  padding: 3.2rem 0;
  font-size: 16px;
  line-height: 1.7;


  > *:not(.datagrid):not(.image-placeholder) {
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
    display: block;
  }



  h2 {
    padding-bottom: 3.2rem;
    padding-bottom: 2rem;


  }

  h3 {
    font-size: 2.2rem;
    padding-bottom: 2rem;
  }

  li {
    list-style-type: initial;
  }

  pre {
    box-shadow: 0 4px 12px 0 rgba(0, 0, 0, 0.05);
    padding: 2.4rem;
    border-radius: 4px;
    background-color: #f6f8fa;
    overflow-x: scroll;
    display: block;
    margin-bottom: 5rem;

    code {
      background-color: #f6f8fa;
    }
  }

  code {
    background: #f3f4f4;
    border-radius: 4px;
    display: inline;
    font-size: 14px;
    padding: .2em .4em;


  }
}
</style>
