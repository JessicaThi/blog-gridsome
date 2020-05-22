<template>
  <Layout>
    <div class="container sm:px-4 mx-auto overflow-x-hidden">
      <div class="flex flex-wrap with-large pt-16 pb-8 mx-4 sm:-mx-4">
        <PostListItem v-for="edge in $page.entries.edges" :key="edge.node.id" :record="edge.node" />
      </div>
      <!-- <div v-if="$page.entries.pageInfo.totalPages > 1" class="pagination flex justify-center mb-8" >
        <Pagination
          :baseUrl="$page.entries.pageInfo.hasNextPage"
          :currentPage="$page.entries.pageInfo.currentPage"
          :totalPages="$page.entries.pageInfo.totalPages"
          :maxVisibleButtons="5"
        />
      </div> -->
    </div>
  </Layout>
</template>

<page-query>

query($page:Int) {

  entries: allBlog(perPage: 9, page: $page, order: ASC) @paginate {
    totalCount
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        title
        excerpt
        image(width:800)
        path
        timeToRead
        humanTime : created(format:"DD MMM YYYY")
        datetime : created
        category {
          id
          title
        }
        tags {
          id
          title
          path
        }
        author {
          id
          name
          image(width:64, height:64, fit:inside)
          path
        }
        place {
          id
          title
          path
        }
      }
    }
  }
}

</page-query>

<script>
import PostListItem from "~/components/PostListItem.vue";
import Pagination from "~/components/Pagination.vue";

export default {
  metaInfo: {
    title: "Blog - Home"
  },
  components: {
    PostListItem,
    Pagination
  }
};
</script>
