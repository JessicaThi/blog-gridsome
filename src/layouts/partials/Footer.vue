<template>
  <nav class="relative bg-black py-4 text-sm text-gray-500">
    <div class="container mx-auto flex flex-wrap justify-between h-12 px-4 items-center">
      <div class="w-full text-center">
      © Copyright {{ currentYear }} by {{ $static.metadata.siteName }} 
      | Design inspired by <a href="https://ghost.org" target="_blank" class="hover:text-white">Ghost</a>
      </div>
      <!-- <div class="w-full md:w-1/2">
      <ul class="list-none flex justify-center ml-0 md:justify-end">

        <li 
          :key="element.name" 
          v-for="(element,index) in $static.metadata.navigation" 
          class="hover:text-white"
          v-bind:class="{'mr-6' : index != Object.keys($static.metadata.navigation).length - 1}"
        >
          <a :href="element.link" v-if="element.external" target="_blank" rel="noopener noreferrer">{{ element.name }}</a>
          <g-link v-else :to="element.link" >{{element.name}}</g-link>
        </li>      
      </ul>
      </div> -->
    </div>
  </nav>
</template>

<static-query>
query {
  metadata {
    siteName
    navigation : footerNavigation {
      name
      link
      external
    }
  }
}
</static-query>

<script>
export default {
  computed: {
    currentYear() {
      return new Date().getFullYear();
    },
  },
};
</script>