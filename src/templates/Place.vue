<template>
    <Layout :hideHeader="true" :disableScroll="true">
    <div class="container sm:pxi-0 mx-auto overflow-x-hidden pt-24">
      <div class="mx-4 sm:mx-0">
        <h1 class="pb-0 mb-0 text-5xl font-medium">{{ $page.place.title }}</h1>
        <p class="text-gray-700 text-xl">
          A collection of
          <span
            class="self-center"
          >{{ $page.place.belongsTo.totalCount }} {{ postLabel }}</span>
        </p>
      </div>

      <div class="pt-8 border-b"></div>

      <div class="flex flex-wrap pt-8 pb-8 mx-4 sm:-mx-4">
        <PostListItem
          v-for="edge in $page.place.belongsTo.edges"
          :key="edge.node.id"
          :record="edge.node"
        />
      </div>

      <div class="pagination flex justify-center mb-8">
        <Pagination
          :baseUrl="$page.place.path"
          :currentPage="$page.place.belongsTo.pageInfo.currentPage"
          :totalPages="$page.place.belongsTo.pageInfo.totalPages"
          :maxVisibleButtons="5"
          v-if="$page.place.belongsTo.pageInfo.totalPages > 1"
        />
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query($id: ID!, $page:Int) {
    place(id: $id) {
      title
      path
      belongsTo(perPage: 5, page: $page) @paginate {
        totalCount
        pageInfo {
          totalPages
          currentPage
        }
        edges {
          node {
            ... on Blog {
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
              place {
                id
                title
                path
              }
            }
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
  components: {
    Pagination,
    PostListItem
  },
  computed: {
    postLabel: function() {
      var pluralize = require("pluralize");
      return pluralize("post", this.$page.place.belongsTo.totalCount);
    }
  },
  metaInfo() {
    return {
      title: this.$page.place.name
    };
  }
};
</script>
