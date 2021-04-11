<template>
  <header>
    <nav class="navbar navbar-light navbar-expand-md">
      <div class="container-fluid">
        <a class="navbar-brand" href="#" style="padding: 10px 20px 15px;">
          <h1>logo</h1>
        </a>
        <div class="collapse navbar-collapse bg-primary d-xl-flex justify-content-md-end" id="navcol-1" style="padding: 20px;">
          <ul class="nav navbar-nav">
            <li class="nav-item" role="presentation">
              <a class="nav-link active text-center text-white" href="#story" @click.prevent="custormAnchor('story')">品牌故事</a>
            </li>
            <li class="nav-item" role="presentation">
              <a class="nav-link text-center text-white" href="#about" @click.prevent="custormAnchor('about')">產品介紹</a>
            </li>
            <li class="nav-item" role="presentation">
              <a class="nav-link text-center text-white" href="#formTable" @click.prevent="custormAnchor('formTable')">保固申請</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>
</template>
<script>
export default {
  data () {
    return {
    }
  },
  methods: {
    custormAnchor (anchorName) {
      const anchorElement = document.getElementById(anchorName)
      if (anchorElement) { anchorElement.scrollIntoView() }
    }
  }
}
</script>
