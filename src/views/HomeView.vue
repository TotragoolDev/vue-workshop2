<template>
  <v-container class="page">
    <hello-world />
  </v-container>
</template>

<script>
  import HelloWorld from '../components/HelloWorld'

  export default {
    name: 'Home',

    components: {
      HelloWorld,
    },
  }
</script>

<style scoped>
  .page {
    display: flex;
    justify-content: center;
    padding-top: 48px;
  }
</style>