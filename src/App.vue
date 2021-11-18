<template>
  <Navbar />
  <router-view/>
</template>

<script>
import Navbar from './components/Navbar.vue'
export default {
  name: "App",
  components: {
    Navbar
  }
}
</script>
<style >
  *{
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
</style>