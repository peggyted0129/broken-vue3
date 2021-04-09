<template>
  <section>
    <article id="story">
      <div class="container-fluid">
        <div style="height: 500px;background: pink">
          <h1 class="mt-15 text-center">story 品牌故事</h1>
          <div class="mt-15" data-aos="fade-up">
            <img style="height: 300px;width: 300px" src="https://upload.cc/i1/2020/12/10/lFshr3.jpg" alt="">
          </div>
        </div>
      </div>
    </article>
    <article class="align-items-xl-center" id="about" style="margin: 5vw 0px;">
      <div class="container align-items-center">
        <div id="about" style="height: 500px;background: red">
          <h1 class="mt-15 text-center">about 產品</h1>
        </div>
      </div>
    </article>
    <div class="container mb-15" id="formTable">
      <form>
        <div class="form-group">
          <label for="exampleInputEmail1">Email address</label>
          <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email">
          <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
        </div>
        <div class="form-group">
          <label for="exampleInputPassword1">Password</label>
          <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
        </div>
        <div class="form-group form-check">
          <input type="checkbox" class="form-check-input" id="exampleCheck1">
          <label class="form-check-label" for="exampleCheck1">Check me out</label>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div>
  </section>
</template>
