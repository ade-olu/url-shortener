<template>
<!-- Created By Oluwatobiloba Adegbaju -->
  <div class="u-s">
    <!-- Top -->
    <div class="top">

      <!-- Nav -->
    <div class="nav">
      <!-- Nav Bar Menu (Mobile) -->
    <div class="hamWrap">
    <div class="menu-wrapper" id="ham">
        <div class="hamburger-menu" v-on:click="menu" v-bind:class="{ animate: isActive }"></div>
    </div>
  </div>

      <ul class="nav-list">
         <!-- Logo -->
        <li class="list l-lg"><a href="index.html" class="lg">
        <img src="../assets/logo.svg" class="logo"/>
        </a></li>
        <!-- Nav Menu (Left) -->
        <li class="list" id="list1"><a href="#features" class="a-list">Features</a></li>
        <li class="list" id="list2"><a href="#" class="a-list">Pricing</a></li>
        <li class="list" id="list3"><a href="#" class="a-list">Resources</a></li>
      </ul>

  <!-- Nav Menu (Right) -->
      <ul class="nav-list-2">
        <li class="list-2" id="list4"><a href="#" class="a-list">Login</a></li>
      </ul>

      <!-- Sign Up Btn -->
      <a href="#" class="a-list">
        <div class="sign-up-bg" id="list5">
          <button class="sign-up">Sign Up</button>
        </div>
          </a>
      </div>
      </div>

      <!-- Mobile Nav -->
      <div class="m-nav" v-bind:class="{ fade: isActive }">
          <ul class="m-nav-list">
        <li class="m-list"><a href="#features" class="a-list" v-on:click="menu">Features</a></li>
        <li class="m-list"><a href="#" class="a-list">Pricing</a></li>
        <li class="m-list"><a href="#" class="a-list">Resources</a></li>
          </ul>

          <div class="h-line"></div>

        <ul class="m-nav-list">
        <li class="m-list"><a href="#" class="a-list">Login</a></li>
        <li class="m-list"><a href="#" class="a-list"><button class="sign-up">Sign Up</button>
        </a></li>
          </ul>
      </div>
      </div>
</template>

<script>
export default {
  name: 'Nav',
  data () {
    return {
      isActive: false
    }
  },
  methods: {
    menu: function () {
      this.isActive = !this.isActive
    }
  }
}
</script>

<!-- SCSS -->
<style scoped lang="scss">
@import "../styles/nav.scss";
</style>
