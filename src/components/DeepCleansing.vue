<template>
  <section>
    <article id="story">
      <div class="mt-16"></div>
      <div class="container-fluid">
        <div style="height: 500px;background: pink" data-aos="fade-up">
          <h1 class="text-center">story 品牌故事</h1>
        </div>
      </div>
    </article>
    <article class="align-items-xl-center" id="about" style="margin: 5vw 0px;">
      <div class="container align-items-center">
        <div id="about" style="height: 500px;background: red">
          <h1 data-aos="fade-up" class="mt-15 text-center">about 產品</h1>
        </div>
        <h1 class="mt-15 text-center" style="height: 200px;background: pink">about 產品2</h1>
      </div>
    </article>
  </section>
</template>
<script>
import AOS from 'aos'
import 'aos/dist/aos.css'

export default {
  mounted () {
    AOS.init({
      offset: 120,
      duration: 3000
    })
  }
}
</script>
