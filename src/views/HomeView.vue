<template>
  <v-container class="page">
    <GradeCalCard />
  </v-container>
</template>

<script>
  import GradeCalCard from '../components/GradeCalCard.vue'

  export default {
    name: 'Home',

    components: {
      GradeCalCard,
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