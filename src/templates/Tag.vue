<template>
  <Layout :hideHeader="true" :disableScroll="true">
    <div class="container min-height-custom lg:pxi-0 mx-auto overflow-x-hidden pt-20 md:pt-24">
      <div class="mx-4 sm:px-4">
        <h1 class="pb-0 mb-0 text-5xl font-medium">{{ $page.tag.title }}</h1>
        <p class="text-gray-700 text-xl">
          Publication de
          <span
            class="self-center"
          >{{ $page.tag.belongsTo.totalCount }} {{ postLabel }}</span>
        </p>
      </div>

      <div class="pt-8 border-b"></div>

      <div class="flex flex-wrap pt-8 pb-8 mx-4">
        <PostListItem
          v-for="edge in $page.tag.belongsTo.edges"
          :key="edge.node.id"
          :record="edge.node"
        />
      </div>

      <div v-if="$page.tag.belongsTo.pageInfo.totalPages > 1" class="pagination flex justify-center mb-8" >
        <Pagination
          :baseUrl="$page.tag.path"
          :currentPage="$page.tag.belongsTo.pageInfo.currentPage"
          :totalPages="$page.tag.belongsTo.pageInfo.totalPages"
          :maxVisibleButtons="5"
        />
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query($id: ID!, $page:Int) {
    tag(id: $id) {
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
      return pluralize("article", this.$page.tag.belongsTo.totalCount);
    }
  },
  metaInfo() {
    return {
      title: this.$page.tag.title
    };
  }
};
</script>
