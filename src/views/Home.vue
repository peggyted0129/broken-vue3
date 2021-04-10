<template>
  <section class="home">
    <NavBar />
    <DeepCleansing />
    <FormTest />
    <Footer />
  </section>
</template>

<script>
import NavBar from '@/components/NavBar.vue'
import DeepCleansing from '@/components/DeepCleansing.vue'
import FormTest from '@/components/FormTest.vue'
import Footer from '@/components/Footer.vue'

export default {
  name: 'Home',
  components: {
    NavBar,
    DeepCleansing,
    FormTest,
    Footer
  }
}
</script>
