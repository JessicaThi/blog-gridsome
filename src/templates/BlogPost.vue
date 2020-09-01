<template>
  <Layout :hideHeader="true" :disableScroll="true">
    <div class="container lg:pxi-0 mx-auto overflow-x-hidden pt-20 md:pt-24">
      <div class="lg:mx-32 md:mx-16 sm:mx-8 mx-4 pt-8">
        <section class="post-header container mx-auto px-0 mb-4 border-b">
          <span class="uppercase text-sm font-medium tracking-wide text-red-500 mt-3">
            <g-link
              :to="$page.blog.category.path"
              class="hover:underline"
            >{{ $page.blog.category.title }}</g-link>
          </span>
          <h1 class="text-5xl font-medium leading-none mt-1">{{ $page.blog.title}}</h1>
          <div class="text-2xl pt-1 pb-4 text-gray-700" v-html="$page.blog.excerpt"></div>
        </section>
        <section class="post-author-list mb-10 mx-0">
          <div class="flex items-center">
            <div class="flex justify-between items-center">
              <ul class="list-none flex author-list">
                <li v-for="author in $page.blog.author" :key="author.id" class="author-list-item">
                  <g-link :to="author.path" v-tooltip="author.name">
                    <g-image
                      :src="author.image"
                      :alt="author.name"
                      class="h-8 w-8 sm:h-10 sm:w-10 rounded-full bg-gray-200 border-2 border-white"
                    />
                  </g-link>
                </li>
              </ul>
            </div>
            <div class="pl-3 flex flex-col text-xs leading-none uppercase">
              <p class="text-gray-700">
                <time :datetime="$page.blog.datetime">{{ $page.blog.humanTime }}</time>
                &nbsp;&middot;&nbsp; {{ $page.blog.timeToRead }} min read
              </p>
              <g-link :to="$page.blog.place.path">
                <p class="text-gray-700 pt-1">📍{{ $page.blog.address.title }}</p>
              </g-link>
            </div>
          </div>
        </section>
      </div>
      <section class="post-image mx-auto w-full">
        <g-image :src="$page.blog.image"></g-image>
        <p class="text-center pt-2">{{ $page.blog.image_caption}}</p>
      </section>
      <div class="lg:mx-32 md:mx-16 px-4 sm:px-0">
        <section class="post-content container mx-auto relative text-gray-700">
          <div class="post-content-text text-xl" v-html="$page.blog.content"></div>
        </section>

        <section class="post-tags container mx-auto relative py-10">
          <g-link
            v-for="tag in $page.blog.tags"
            :key="tag.id"
            :to="tag.path"
            class="text-sm rounded-full py-2 px-3 mr-1 font-medium text-yellow-200 bg-orange-400 bg-opacity-85 hover:text-red-500 hover:border-yellow-500"
          >#{{ tag.title }}</g-link>
        </section>
      </div>
    </div>

    <section class="post-related bg-black text-gray-200 pt-10 px-4 border-b border-b-gray-900">
      <div class="container mx-auto">
        <div class="flex flex-wrap pt-8">
          <PostListItem v-if="$page.previous" :record="$page.previous" :border=false></PostListItem>
          <PostListItem v-if="$page.next" :record="$page.next" :border=false></PostListItem>
        </div>
      </div>
    </section>
  </Layout>
</template>

<page-query>
  query($id: ID!, $previousElement: ID!, $nextElement: ID!) {
    blog(id: $id) {
      title
      path
      image(width:1600, height:800)
      image_caption
      excerpt
      content
      humanTime : created(format:"DD MMMM YYYY")
      datetime : created(format:"ddd MMM DD YYYY hh:mm:ss zZ")
      timeToRead
      tags {
        id
        title
        path
      }
      category {
        id
        title
        path
        belongsTo(limit:4) {
          totalCount
          edges {
            node {
              ... on Blog {
                title
                path
              }
            }
          }
        }
      }
      author {
        id
        name
        image
        path
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
      address {
        id
        title
      }
    }

    previous: blog(id: $previousElement) {
      title
      excerpt
      image(width:800)
      path
      timeToRead
      category {
        id
        title
      }
      author {
        id
        name
        image(width:64, height:64, fit:inside)
        path
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

    next: blog(id: $nextElement) {
      title
      excerpt
      image(width:800)
      path
      timeToRead
      category {
        id
        title
      }
      author {
        id
        name
        image(width:64, height:64, fit:inside)
        path
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
</page-query>

<script>
import PostListItem from "~/components/PostListItem.vue";

export default {
  components: {
    PostListItem,
  },
  metaInfo() {
    return {
      title: this.$page.blog.title,
    };
  },
};
</script>