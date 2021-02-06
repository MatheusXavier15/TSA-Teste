<template>
  <div class="home">
    <Register/>
    <Footer/>
  </div>
</template>

<script>
// @ is an alias to /src

import Register from './../components/register.vue'
import Footer from './../components/footer.vue'

export default {
  name: 'Home',
  components: {
    Register,
    Footer
  }
}
</script>
