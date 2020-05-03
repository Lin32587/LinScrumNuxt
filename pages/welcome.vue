<template>
  <div class="mx-auto mt-10">
    <div class="row">
      <div class="col-md-6 col-sm-12 logo">
        <img src="../static/Logo.png" height=250px />
      </div>
      <div class="col-md-6 col-sm-12">
        <p class="logotitle">LinScrum</p>
        <p class="subtitle">PROGRAM MANAGEMENT</p>
      </div>
    </div>
  <div class="col-12 mt-md-10">
    <h2>一个轻量化的软件开发项目管理工具</h2>
  </div>
  </div>
</template>

<script>
export default {
  layout: "welcomelayout",
  name:"Welcome",
};
</script>

<style>
h2{
  text-align: center;
  color: #1890FF;
}
.logo{
  height: 60%;
}
img{
  display: block;
  text-align: center;
  margin: auto;
}
p.logotitle{
  margin-top: 2rem;
  display: block;
  font-size: 450%;
  font-style: oblique;
  color: teal;
  font-weight:bold;
  text-align: center;
}
.subtitle{
  color: #1890FF;
  font-weight: bold;
  margin-top: -20px;
  letter-spacing: 10px;
  white-space:nowrap;
  text-align: center;
}

@media screen and (max-width: 800px) {
  img{
    height: 180px;
  }
  p.logotitle{
    font-size: 280%;
  }
  .subtitle{
    letter-spacing: 8px;
  }
}
</style>
