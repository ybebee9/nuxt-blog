<template>
    <!-- Main Content -->
  <div class="container">
    <div class="row">
      <div class="col-lg-8 col-md-10 mx-auto">
        <PostList    v-for="blog in paginatedData"
                     :key="blog.name"
                     :blog="blog"></PostList>
        <div class="btn-cover">
          <button :disabled="pageNum === 0" @click="prevPage">
            Previous
          </button>
          <span class="page-count">{{ pageNum + 1 }} / {{ pageCount }}</span>
          <button :disabled="pageNum >= pageCount - 1" @click="nextPage" >
            Next
          </button>
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
  data () {
    return {
      pageNum: 0
    }
  },
  props: {
      blogs: {
        type: Array
      },
      pageSize: {
        type: Number,
        required: false,
        default: 2
      }
    },
    methods: {
      nextPage () {
        this.pageNum += 1;
      },
      prevPage () {
        this.pageNum -= 1;
      }
    },
    computed: {
      pageCount () {
        let listLeng = this.blogs.length,
            listSize = this.pageSize,
            page = Math.floor(listLeng / listSize);
        if (listLeng % listSize > 0) page += 1;

      return page;
      },
      paginatedData () {
        const start = this.pageNum * this.pageSize,
              end = start + this.pageSize;
        return this.blogs.slice(start, end);
      }
  }
}

</script>
<style scoped>
  .btn-cover {
    padding-left: 0;
    margin: 20px 0;
    text-align: center;
    list-style: none
  }
  .btn-cover button {
    display: inline
  }
  .btn-cover span {
    display: inline
  }
  .btn-cover button {
    font-size: 14px;
    padding: 5px 14px;
    display: inline-block;
    background-color: #fff;
    border: 1px solid #ddd;
    border-radius: 15px;
    color: #007bff;
    font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;
  }
  .btn-cover span {
    font-size: 16px;
    padding: 5px 14px;
    display: inline-block;
    border-radius: 15px;
    color: #555555;
    font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;
  }
  .btn-cover button:focus, .btn-cover button:hover {
    text-decoration: none;
    background-color: #eee
  }
  .pager {
    padding-left: 0;
    margin: 20px 0;
    text-align: center;
    list-style: none
  }
  .pager li {
    display: inline
   }
  .pager li > a, .pager li > span {
    font-size: 14px;
    padding: 5px 14px;
    display: inline-block;
    background-color: #fff;
    border: 1px solid #ddd;
    border-radius: 15px;
    color: #007bff;
    font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;
    }
  .pager li > a:focus, .pager li > a:hover {
    text-decoration: none;
    background-color: #eee;
  }
</style>
