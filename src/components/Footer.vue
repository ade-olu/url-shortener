<template>
<div class="u-s">
<!-- Footer -->
<div class="footer">
  <!-- Footer Text -->
  <div class="ft-text">
    <!-- Logo -->
    <a href="index.html" class="lg-2">
  <img src="../assets/logo-2.svg" class="logo-2"/>
    </a>
  <!-- Features (Footer) -->
      <ul class="f-l">
        <li class="l-ft h-ft"><a href="#" class="a-ft"><b>Features</b></a></li>
        <li class="l-ft"><a href="#urlShortener" class="a-ft">Link Shortening</a></li>
        <li class="l-ft"><a href="#" class="a-ft">Branded Links</a></li>
        <li class="l-ft"><a href="#features" class="a-ft">Analytics</a></li>
      </ul>
      <!-- Resources (Footer) -->
      <ul class="f-l">
        <li class="l-ft h-ft"><a href="#" class="a-ft"><b>Resources</b></a></li>
        <li class="l-ft"><a href="#" class="a-ft">Blog</a></li>
        <li class="l-ft"><a href="#" class="a-ft">Developers</a></li>
        <li class="l-ft"><a href="#" class="a-ft">Support</a></li>
      </ul>
      <!-- Company (Footer) -->
      <ul class="f-l">
        <li class="l-ft h-ft"><a href="#" class="a-ft"><b>Company</b></a></li>
        <li class="l-ft"><a href="#" class="a-ft">About</a></li>
        <li class="l-ft"><a href="#" class="a-ft">Our Team</a></li>
        <li class="l-ft"><a href="#" class="a-ft">Careers</a></li>
        <li class="l-ft"><a href="#" class="a-ft">Content</a></li>
      </ul>
  <!-- Footer Icons -->
  <div class="ft-i">
    <!-- FaceBook -->
    <a href="#">
    <i class="fab fa-facebook-square ft-i-1"></i>
    </a>
    <!-- Twitter -->
    <a href="https://twitter.com/_ade_olu" target="_blank">
    <i class="fab fa-twitter ft-i-2"></i>
    </a>
    <!-- Pinterest -->
    <a href="#">
    <i class="fab fa-pinterest ft-i-3"></i>
    </a>
    <!-- Instagram -->
    <a href="https://instagram.com/ade._olu" target="_blank">
    <i class="fab fa-instagram ft-i-4"></i>
    </a>
  </div>
</div>
</div>
</div>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<!-- SCSS -->
<style scoped lang="scss">
// Font Link
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@500;700&display=swap');

// Colors
$cyan: hsl(180, 66%, 49%);
$dark-violet: hsl(257, 27%, 26%);
$red: hsl(0, 87%, 67%);
$gray: hsl(0, 0%, 75%);
$light-violet: hsl(230, 25%, 95%);
$grayish-violet: hsl(257, 7%, 63%);
$v-dark-blue: hsl(255, 11%, 22%);
$v-dark-violet: hsl(260, 8%, 14%);

// Font
$font: 'Poppins', sans-serif;

.u-s {
  font-family: $font;
  font-size: 18px;
  overflow: hidden;
}

a {
    text-decoration: none;
}

// Footer
.footer {
  position: relative;
  width: 100%;
  height: auto;
  padding: 3em 9% 3em 9% !important;
  background: $v-dark-violet;
  color: #fff;
}

.lg-2 {
    -webkit-tap-highlight-color: transparent !important;
}

.logo-2 {
  width: 121px !important;
  height: 33px !important;
  margin-right: 6em !important;
}

.ft-text {
  display: flex;
  flex-direction: row;
}

.f-l, .r-l, .c-l {
  list-style-type: none;
  margin-left: 4em !important;
}

.f-l li a {
    -webkit-tap-highlight-color: transparent !important;
}

.a-ft {
  font-size: 16px;
  color: $gray;
}

.h-ft {
  margin-bottom: 0.8em !important;
}

.h-ft a {
  color: #fff !important;
}

// Footer Icons
.ft-i {
  display: flex;
  flex-direction: row;
  margin-left: 8% !important;
}

.ft-i a {
    -webkit-tap-highlight-color: transparent !important;
}

.ft-i-1, .ft-i-2, .ft-i-3, .ft-i-4 {
  margin-left: 1em !important;
  font-size: 24px;
  color: #fff;
  transition: all 250ms ease !important;

&:active {
    transform: scale(0.98) !important;
}
}

// Media Queries
// 1440px Width & 900px Height
@media (max-width: 1440px) and (max-height: 900px) {
.logo-2 {
  margin-right: 10em !important;
  }

  // Footer Icons
.ft-i {
  margin-left: 12% !important;
  }
}

// 1440px
@media screen and (max-width: 1440px) {
    .logo-2 {
  margin-right: 6em !important;
  }

  // Footer Icons
.ft-i {
  margin-left: 8% !important;
  }
}

// 1024px
@media screen and (max-width: 1024px) {
    // Footer
  .logo-2 {
  margin-right: 3.4em !important;
  }

  .f-l, .r-l, .c-l {
  margin-left: 2em !important;
}

  // Footer Icons
.ft-i {
  margin-left: 3.4em !important;
  }
}

// 768px
@media screen and (max-width: 768px) {
    // Footer
  .footer {
  padding: 3em 0em 3em 0em !important;
}

.ft-text {
  display: flex;
  flex-direction: column;
  text-align: center !important;
}

.logo-2 {
  margin: 0 auto !important;
}

  .f-l, .r-l, .c-l {
  margin-top: 2em !important;
  margin-left: 0em !important;
}

  // Footer Icons
.ft-i {
  margin: 2em auto 0 auto !important;
  }

.ft-i-1 {
  margin-left: 0em !important;
  }
}

// 320px
@media screen and (max-width: 320px) {
  .u-s {
    display: none;
  }
}
</style>
