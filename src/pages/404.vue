<template>
  <Layout :hideHeader="true" :disableScroll="true">
    <div class="container min-height-custom mx-auto pb-16 px-4 sm:px-0 pt-20 md:pt-24">
      <div class="lg:mx-32 md:mx-16 sm:mx-8">
        <h1 class="pb-4 text-5xl font-medium break-normal">Cette page n'existe pas.</h1>
        <p>Oups ! Tu t'es égaré reviens à la <g-link to="/" class="text-orange-500">page d'accueil</g-link></p>
      </div>
    </div>
  </Layout>
</template>

<script>
export default {
  metaInfo: {
    title: "Page error"
  }
};
</script>
