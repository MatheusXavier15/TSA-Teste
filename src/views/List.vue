<template>
  <div class="List">
    <List/>
    <Footer/>
  </div>
</template>

<script>

import List from './../components/list.vue'
import Footer from './../components/footer.vue'

export default {
  name: 'list',
  components: {
    List,
    Footer    
  }
}
</script>