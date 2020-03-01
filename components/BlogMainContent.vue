<template>
    <!-- Main Content -->
  <div class="container">
    <div class="row">
      <div class="col-lg-8 col-md-10 mx-auto">
        <PostList    v-for="blog in paginatedData"
                     :key="blog.name"
                     :blog="blog"></PostList>
        <!-- Pager -->
        <div class="btn-cover">
          <button :disabled="pageNum === 0" @click="prevPage" class="page-btn">
            이전
          </button>
          <span class="page-count">{{ pageNum + 1 }} / {{ pageCount }} 페이지</span>
          <button :disabled="pageNum >= pageCount - 1" @click="nextPage" class="page-btn">
            다음
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
        console.log('nextPage' + this.pageNum);
      },
      prevPage () {
        this.pageNum -= 1;
        console.log('prevPage' + this.pageNum);
      }
    },
    computed: {
      pageCount () {
        let listLeng = this.blogs.length,
            listSize = this.pageSize,
            page = Math.floor(listLeng / listSize);
        if (listLeng % listSize > 0) page += 1;

        /*
        아니면 page = Math.floor((listLeng - 1) / listSize) + 1;
        이런식으로 if 문 없이 고칠 수도 있다!
        */
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
