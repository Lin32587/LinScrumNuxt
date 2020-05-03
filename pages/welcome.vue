<template>
  <div class="mx-auto mt-10">
    <div class="row">
      <div class="col-md-6 col-sm-12 logo">
        <img class="logoimg" src="../static/Logo.png" height="250px" />
      </div>
      <div class="col-md-6 col-sm-12">
        <p class="logotitle">LinScrum</p>
        <p class="subtitle">PROGRAM MANAGEMENT</p>
        <v-btn
          class="ma-2 mt-10 d-none d-sm-flex"
          outlined
          href="https://github.com/Lin32587/LinScrumNuxt"
        >
          <v-icon left>mdi-github</v-icon>github
        </v-btn>
      </div>
    </div>
    <div class="col-12 mt-md-10">
      <h2>一个轻量化的软件开发项目管理工具</h2>
    </div>

    <div class="col-12 mt-12 ">
      <p class="power">Powered by</p>
      <div class="row">
        <div class="col-md-3 col-sm-6">
          <a href="https://docs.microsoft.com/zh-cn/dotnet/core/">
            <img src="../static/1200px-.NET_Core_Logo.svg.png" alt=".NET Core" width="100px" height="100px" />
          </a>
        </div>
        <div class="col-md-3 col-sm-6">
          <a href="https://zh.nuxtjs.org/">
            <img src="../static/Nuxt.png" alt="Nuxt.js" width="100px" height="100px" />
          </a>
        </div>
        <div class="col-md-3 col-sm-6">
          <a href="https://vuetifyjs.com/zh-Hans/">
            <img src="../static/Vuetify.svg" alt="Vuetify" width="100px" height="100px" />
          </a>
        </div>
        <div class="col-md-3 col-sm-6">
          <a href="https://cn.vuejs.org/">
            <img src="../static/Vue.png" alt="Vue" width="100px" height="100px" />
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  layout: "welcomelayout",
  name: "Welcome"
};
</script>

<style>
h2 {
  text-align: center;
  color: #1890ff;
}
.power {
  text-align: center;
  font-weight: bolder;
}
.logo {
  height: 60%;
}
img.logoimg {
  display: block;
  text-align: center;
  margin: auto;
}
p.logotitle {
  margin-top: 2rem;
  display: block;
  font-size: 450%;
  font-style: oblique;
  color: teal;
  font-weight: bold;
  text-align: center;
}
.subtitle {
  color: #1890ff;
  font-weight: bold;
  margin-top: -20px;
  letter-spacing: 10px;
  white-space: nowrap;
  text-align: center;
}

@media screen and (max-width: 800px) {
  img {
    height: 180px;
  }
  p.logotitle {
    font-size: 280%;
  }
  .subtitle {
    letter-spacing: 8px;
  }
}
</style>
