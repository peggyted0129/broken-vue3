<template>
  <section class="home">
    <NavBar />
    <DeepCleansing />
    <Footer />

    <aside class="container">
      <div class="row">
        <div class="col">
          <a href="#register">
            <img class="register_button" src="../assets/img/register_button.svg">
          </a>
        </div>
      </div>
    </aside>
  </section>
</template>

<script>
import NavBar from '@/components/NavBar.vue'
import DeepCleansing from '@/components/DeepCleansing.vue'
import Footer from '@/components/Footer.vue'

export default {
  name: 'Home',
  components: {
    NavBar,
    DeepCleansing,
    Footer
  }
}
</script>
