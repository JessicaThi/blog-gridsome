<template>
  <div
    class="flex flex-post px-0 sm:px-4 pb-8 mb-8"
    v-bind:class="{ 'no-border': !border }"
  >
    <g-link :to="record.path" class="post-card-image-link">
      <g-image
        :src="record.image"
        :alt="record.title"
        quality="85"
        class="post-card-image"
      ></g-image>
    </g-link>
    <div class="post-card-content">
      <g-link :to="record.path">
        <p
          class="uppercase text-xs font-medium tracking-wide text-red-500 mt-3"
        >
          {{ record.category.title }}
        </p>
        <h2 class="post-card-title mt-0 mb-3">
          {{ record.title }}
        </h2>
        <p class="post-card-excerpt">{{ record.excerpt }}</p>
      </g-link>
      <g-link :to="record.place.path">
        <p class="text-sm">📍{{ record.place.title }}</p>
      </g-link>
      <div class="pt-4">
        <g-link
          v-for="tag in record.tags"
          :key="tag.id"
          :to="tag.path"
          class="text-sm rounded-full py-2 px-3 mr-1 font-medium text-yellow-200 bg-orange-400 bg-opacity-85 hover:text-red-500 hover:border-yellow-500"
          >#{{ tag.title }}</g-link
        >
      </div>
      <!-- <div class="w-full post-card-meta pt-4">
      <div class="avatars">
        <div class="flex items-center">
          <div class="flex justify-between items-center">
            <ul class="list-none flex author-list">
              <li v-for="author in record.author" :key="author.id" class="author-list-item">
                <g-link :to="author.path">
                  <g-image
                    :src="author.image"
                    :alt="author.name"
                    class="w-8 h-8 rounded-full bg-gray-200 border-2 border-white"
                  />
                </g-link>
              </li>
            </ul>
          </div>
          <div class="ml-3 pl-3 border-l flex flex-col text-xs leading-none uppercase">
             <p>
               <time
          
          :datetime="record.datetime"
        >{{ record.humanTime }}</time>
             </p>
             <p>
               {{ record.timeToRead }} min
             </p>
          </div>
        </div>
       
      </div>

      </div> -->
    </div>
  </div>
</template>

<script>
export default {
  props: {
    record: {},
    border: {
      type: Boolean,
      default: true,
    },
  },
};
</script>

<style></style>
