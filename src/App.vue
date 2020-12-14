<template>
  <div>
    <Navbar />
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';
export default {
  name: 'App',
  components: {
    Navbar,
  },
  mounted(){
    this.$store.dispatch('traerData');
  },
}
</script>

<style lang="scss">

</style>
