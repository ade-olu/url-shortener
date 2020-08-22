<template>
<!-- Created By Oluwatobiloba Adegbaju -->
  <div class="u-s">
    <div class="inner">
    <!-- Top -->
    <div class="top">

        <!-- Illustration -->
         <img src="../assets/illustration-working.svg" class="i-w"/>

         <!-- Text -->
         <div class="text">
           <h1 class="h">More than just <br class="t-br"> shorter links</h1>
           <p class="b">Build your brand's recognition and <br class="t-br-2"> get detailed <br class="t-br-1"> insights on how your <br class="t-br-2"> links are performing.</p>
          <br>
          <!-- Get Started Btn -->
          <a href="#urlShortener" class="a-gs">
          <button class="g-s">Get Started</button>
          </a>
         </div>
    </div>

    <!-- Middle -->
    <div class="middle">
      <div class="mid" id="urlShortener">
        <div class="u-s-div">
          <form @submit.prevent="trimUrl">
        <!-- URL Shortener Input -->
        <input class="u-s-i" type="text" placeholder="Shorten a link here..." v-model="url" required>
          <!-- Shorten Button -->
          <button class="s">Shorten It!</button>
          </form>
        </div>
        <!-- Bg Design -->
        <div class="m-bg"></div>
      </div>
      </div>

      <!-- Spacing Div -->
      <div class="space">
      </div>

      <!-- Shortened Links -->
      <div class="sh-con">  
      <div class="sh-l-bg">
      <div class="s-links-bg" v-if="isReady">
        <div class="s-links-div">
        <a :href="parsedUrl" target="_blank" class="a-sh-links"><p class="sh-links">{{ parsedUrl }}</p></a>
          <!-- Copy Button -->
          <div class="cy-bg">
          <button class="cy" v-clipboard:copy="parsedUrl" v-clipboard:success="onCopy" v-bind:class="{ change: isActive }">
            <span v-if="!isLoading && !copied">Copy</span>
            <span v-if="copied">Copied!</span>
          </button>
          </div>
        </div>
      </div>

      <!-- Links -->
      <div class="sh-l-bg-2">
      <div class="s-links-bg-2" v-for="link in links" :key="link">
      <ul class="ul-s-links">
        <li class="l-s-links">
          <a :href="link" target="_blank" class="a-sh-links-2">{{ link }}</a></li>
      </ul>
      </div>
      </div>

      <!-- Spacing Div -->
      <div class="space">
      </div>
      
      </div>
      
      </div>

    <!-- Bottom -->
    <div class="bottom">
      <!-- Features -->
      <div id="features">
      <div class="text-2">
           <h1 class="h-2">Advanced Statistics</h1>
           <p class="b-2">Track how your links are performing across the web with <br class="t-2-br-1"> our advanced statistics dashboard.</p>
    </div>
    <div class="f">
      <!-- Bg Line -->
      <div class="bg-l"></div>
      <!-- Feature 1 -->
      <div class="f-1">
        <!-- Icon 1 -->
        <div class="i-bg">
          <img src="../assets/icon-brand-recognition.svg" class="f-i"/>
        </div>
        <!-- Feature Text -->
        <h3 class="f-h">Brand Recognition</h3>
        <p class="f-b">Boost your brand recognition with each click. Generic links don't mean a thing. Branded links help instil confidence in your content.</p>
      </div>
      <!-- Feature 2 -->
      <div class="f-2">
        <!-- Icon 2 -->
        <div class="i-bg">
          <img src="../assets/icon-detailed-records.svg" class="f-i"/>
        </div>
        <!-- Feature Text -->
        <h3 class="f-h">Detailed Records</h3>
        <p class="f-b">Gain insights into who is clicking your links. Knowing when and where people engage with your content helps inform better decisions.</p>
      </div>
      <!-- Feature 3 -->
      <div class="f-3">
        <!-- Icon 3 -->
        <div class="i-bg">
          <img src="../assets/icon-fully-customizable.svg" class="f-i"/>
        </div>
        <!-- Feature Text -->
        <h3 class="f-h">Fully Customizable</h3>
        <p class="f-b">Improve brand awareness and content discoverability through customizable links, supercharging audience engagement.</p>
      </div>
      </div>
      </div>
  </div>

  <!-- Boost -->
  <div class="boost">
    <!-- Bg Design -->
        <div class="b-bg"></div>
        <!-- Content -->
        <div class="b-con">
          <h1 class="b-text">Boost your links today</h1>
          <!-- Get Started Btn -->
          <div class="b-btn">
          <a href="#urlShortener" class="a-gs">
          <button class="g-s-2">Get Started</button>
          </a>
          </div>
        </div>
  </div>
  </div>

  <!-- If Not Responsive -->
  <div class="n-res">
    <h3 class="n-res-h">Not Responsive</h3>
  </div>

  </div>
</template>

<script>
export default {
  name: 'UrlShortener',
  data() {
        return {
            url: '',
            isLoading: false,
            isReady: false,
            parsedUrl: '',
            error: false,
            errorMessage: '',
            copied: '',
            links: [],
            copyText: 'Copy',
            isActive: false
        }
    },
    methods: {
        trimUrl() {
            this.isLoading = true;
            this.isReady = false;
            this.$http.post('https://rel.ink/api/links/', {"url": this.url})

            .then(res=> {
                this.isLoading = false;
                this.parsedUrl = `https://rel.ink/${res.body.hashid}`;
                this.isReady = true;
                this.links.push(this.parsedUrl);
                localStorage.setItem("links", JSON.stringify(this.links));
            })
            .catch(err => {
                this.errorMessage = err;
                this.error = true;
                console.log(err)
            })
            
        },
        onCopy() {
            this.copied = true;
            this.isActive = !this.isActive
            setTimeout(()=> {
                this.copied = false;
                this.isActive = !this.isActive
            }, 2500)
        },
        getLinks() {       
            if (localStorage.getItem('links')) this.links = JSON.parse(localStorage.getItem('links'));
        }
    },
    mounted() {
        this.getLinks();
}
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
  overflow-x: hidden;
}

.n-res {
  display: none;
}

// Top Div
.top {
  position: relative;
  width: 100%;
  height: auto;
  padding-bottom: 8% !important;
}

// Bottom Div
.bottom {
  position: relative;
  width: 100%;
  height: auto;
  background: $light-violet;
  padding-bottom: 18% !important;
}

.a {
  text-decoration: none;
  -webkit-tap-highlight-color: transparent !important;
}

button {
  -webkit-tap-highlight-color: transparent !important;
}

// Illustration
.i-w {
  position: relative;
  top: 0;
  left: 120%;
  transform: translate(-120%, 0) !important;
}

// Text
.text {
  width: 34%;
  position: absolute;
  top: 8%;
  left: 12.4%;
  transform: translate(-12.4%, 8%) !important;
}

.h {
  font-size: 3.5rem;
  color: $v-dark-blue;
  line-height: 1.2 !important;
  margin-bottom: 0.2em !important;
}

.b {
  width: 100% !important;
  color: $grayish-violet;
  margin-bottom: 0.4em !important;
}

.t-br-2 {
  display: none;
}

// Get Started Btn
.a-gs {
  -webkit-tap-highlight-color: transparent !important;
}
.g-s {
  width: auto;
  height: auto;
  padding: 0.6em 2em 0.6em 2em !important;
  border-radius: 30px;
  font-family: $font;
  font-size: 18px;
  font-weight: 700;
  cursor: pointer;
  background: $cyan;
  color: #fff !important;
  text-align: center !important;
  border: 0px solid transparent !important;
  outline: none !important;
  transition: all 250ms ease !important;

  &:hover {
    opacity: 0.6 !important;
  }

&:active {
    transform: scale(0.98) !important;
}
}

.middle {
  background-image: linear-gradient(#fff 50%, $light-violet 50%);
}

.mid {
  position: relative;
  width: 82%;
  height: 8em;
  background: $dark-violet;
  margin: 0 8% 0 8% !important;
  border-radius: 8px;
}

.m-bg {
  width: 100%;
  height: 100%;
  border-radius: 8px;
  background-image: url(../assets/bg-shorten-desktop.svg);
  background-size: 100% 100% !important;
  background-repeat: no-repeat;
}

.u-s-div {
  position: absolute;
  width: 92%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) !important;
  z-index: 1 !important;
}

// Input
.u-s-i {
  outline: none !important;
  border: 0 solid transparent;
  border-radius: 8px;
  width: 36em !important;
  height: auto;
  padding: 0.6em 0 0.6em 1em !important;
  font-family: $font;
  font-size: 18px;
  font-weight: 500;
  margin-left: 2em !important;
  color: $v-dark-violet !important;
}

// Shorten It Btn
.s {
  width: auto;
  height: auto;
  padding: 0.6em 2em 0.6em 2em !important;
  border-radius: 8px;
  font-family: $font;
  font-size: 18px;
  font-weight: 700;
  cursor: pointer;
  background: $cyan;
  color: #fff !important;
  text-align: center !important;
  border: 0px solid transparent !important;
  outline: none !important;
  margin-left: 2em !important;
  transition: all 250ms ease !important;

  &:hover {
    opacity: 0.8 !important;
  }

&:active {
    transform: scale(0.98) !important;
}
}

// Shortened Links
.sh-l-bg, .sh-l-bg-2 {
  background: $light-violet;
}

.s-links-bg {
  position: relative;
  width: 82%;
  height: 5em;
  background: #fff;
  margin: 0 8% 2em 8% !important;
  border-radius: 8px;
}

.s-links-div {
  position: absolute;
  width: 92%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) !important;
}

.sh-links {
  font-size: 18px;
}

.a-sh-links {
  text-decoration: none !important;
  color: $cyan;
}

// Copy Btn
.cy-bg {
  position: absolute;
  top: 50%;
  right: 0% !important;
  transform: translate(0%, -50%) !important;
}

.cy {
  width: auto;
  height: auto;
  padding: 0.6em 2em 0.6em 2em !important;
  border-radius: 8px;
  font-family: $font;
  font-size: 18px;
  font-weight: 700;
  cursor: pointer;
  background: $cyan;
  color: #fff !important;
  text-align: center !important;
  border: 0px solid transparent !important;
  outline: none !important;
  transition: all 250ms ease !important;

  &:hover {
    opacity: 0.6 !important;
  }

&:active {
    transform: scale(0.98) !important;
}
}

.change {
  background: $dark-violet;
}

// Spacing Div
.space {
  width: 100%;
  height: auto;
  background: $light-violet;
  padding: 0 0 2em 0 !important;
}

// Links Div
.s-links-bg-2 {
  position: relative;
  width: 82%;
  height: auto;
  background: #fff;
  padding: 1.5em 0 1.5em 0 !important;
  margin: 0 8% 2em 8% !important;
  border-radius: 8px;
}

.ul-s-links {
  list-style-type: none;
}

.a-sh-links-2 {
  text-decoration: none !important;
  color: $cyan;
  margin-left: 2em !important;
}

// Text 2
.text-2 {
 text-align: center;
}

.h-2 {
  color: $v-dark-blue;
  padding-top: 0.5em !important;
  margin-bottom: 0.2em !important;
}

.b-2 {
  color: $grayish-violet;
}

// Features
.f {
  position: relative;
  display: flex;
  flex-direction: row;
  margin-top: 5em !important;
}

.f-1, .f-2, .f-3 {
  width: 28%;
  height: auto;
  background: #fff;
  margin-left: 2.5em !important;
  border-radius: 8px;
  padding: 1.5em 1.5em 1.5em 1.6em !important;
  z-index: 1 !important;
}

.f-1 {
  margin-left: 9% !important;
}

.f-2 {
  margin-top: 4% !important;
  margin-bottom: -4% !important;
}

.f-3 {
  margin-right: 9% !important;
  margin-top: 8% !important;
  margin-bottom: -8% !important;
}

.f-h {
  color: $v-dark-blue;
  margin-bottom: 0.5em !important;
}

.f-b {
  color: $grayish-violet;
  font-size: 16px;
}

.i-bg {
  position: relative;
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background: $dark-violet;
  margin-top: -25% !important;
  margin-bottom: 1.5em !important;
}

.f-i {
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) !important;
}

.bg-l {
  position: absolute;
  top: 74%;
  left: 50%;
  transform: translate(-50%, -74%) !important;
  width: 82%;
  height: 0.6em;
  background: $cyan;
}

// Boost
.boost {
  position: relative;
  width: 100%;
  height: 12em;
  background: $dark-violet;
}

.b-bg {
  width: 100%;
  height: 100%;
  background-image: url(../assets/bg-boost-desktop.svg);
  background-size: 100% 100% !important;
  background-repeat: no-repeat;
}

.b-con {
  position: absolute;
  top: 25%;
  left: 50%;
  transform: translate(-50%, -25%) !important;
}

.b-text {
  color: #fff;
}

.b-btn {
  position: absolute;
  top: 70%;
  left: 50%;
  transform: translate(-50%, 70%) !important;
}

.g-s-2 {
  width: auto;
  height: auto;
  padding: 0.6em 2em 0.6em 2em !important;
  border-radius: 30px;
  font-family: $font;
  font-size: 18px;
  font-weight: 700;
  cursor: pointer;
  background: $cyan;
  color: #fff !important;
  text-align: center !important;
  border: 0px solid transparent !important;
  outline: none !important;
  transition: all 250ms ease !important;

&:active {
    transform: scale(0.98) !important;
}
}

// Media Queries
// 1024px
@media screen and (max-width: 1024px) {
  .i-w {
    width: 600px !important;
    height: auto !important;
  }

// Text
.text {
  width: 40%;
}

  .h {
  font-size: 3.2rem;
  color: $v-dark-blue;
  line-height: 1.2 !important;
  margin-bottom: 0.2em !important;
}

.b {
  width: 100% !important;
  color: $grayish-violet;
  margin-bottom: 0.4em !important;
  }

  .t-br, .t-br-1 {
  display: none;
}

.mid {
  position: relative;
  width: 82%;
  height: 12em;
  background: $dark-violet;
  margin: 0 8% 0 8% !important;
  border-radius: 8px;
  }

.u-s-div {
  position: absolute;
  width: 92%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) !important;
  z-index: 1 !important;
}

  // Input
.u-s-i {
  width: 36em !important;
  height: auto;
  padding: 0.6em 0 0.6em 1em !important;
}

// Shorten It Btn
.s {
  margin-top: 1em !important;
  width: auto;
  height: auto;
  padding: 0.6em 2em 0.6em 2em !important;
  }

  .bg-l {
  position: absolute;
  top: 62%;
  left: 50%;
  transform: translate(-50%, -62%) !important;
  }
}

// 768px
@media screen and (max-width: 768px) {
// Illustration
.i-w {
  position: relative;
  top: 0;
  left: 50%;
  transform: translate(-50%, 0) !important;
}

// Text
.text {
  width: 100%;
  margin-top: 2em !important;
  position: relative;
  top: 0%;
  left: 0%;
  transform: translate(0%, 0%) !important;
  text-align: center !important;
  }

  .t-br, .t-br-1 {
  display: block;
}

  .mid {
    margin-top: 3em !important;
  }

  // Input
.u-s-i {
  width: 27em !important;
  height: auto;
  padding: 0.6em 0 0.6em 1em !important;
}

// Shorten It Btn
.s {
  margin-top: 1.5em !important;
  width: auto;
  height: auto;
  padding: 0.6em 2em 0.6em 2em !important;
  }

  // Shortened Links
  .s-links-bg {
    height: 8em !important;
  }

  .sh-links {
  position: relative;
  margin-left: 0.8em !important;
  }

  // Copy Btn
.cy-bg {
  position: relative;
  top: 0%;
  right: 0% !important;
  transform: translate(0%, 0%) !important;
  margin-top: 1em !important;
  margin-left: 0.8em !important;
}

  // Features
.f {
  position: relative;
  display: flex;
  flex-direction: column;
  margin-top: 5em !important;
}

.f-1, .f-2, .f-3 {
  width: 36%;
  height: auto;
  background: #fff;
  margin-left: 0em !important;
  z-index: 1 !important;
}

.f-1 {
  margin: 0 auto !important;
}

.f-2 {
  margin: 10% auto 0 auto !important;
}

.f-3 {
  margin: 10% auto 0 auto !important;
}

.f-h {
  color: $v-dark-blue;
  margin-bottom: 0.5em !important;
  text-align: center !important;
}

.f-b {
  color: $grayish-violet;
  font-size: 16px;
  text-align: center !important;
}

.i-bg {
  margin-top: -25% !important;
  margin-left: auto !important;
  margin-right: auto !important;
  margin-bottom: 1.5em !important;
}

.bg-l {
  position: absolute;
  top: 5em;
  left: 50%;
  transform: translate(-50%, -5em) !important;
  width: 0.6em;
  height: 82%;
  background: $cyan;
  }

  .b-con {
  width: 100% !important;
  }

  .b-text {
    text-align: center !important;
  }
}

// 414px
@media screen and (max-width: 414px) {
  // Top Div
  .top {
    padding-bottom: 10% !important;
  }

// Illustration
.i-w {
  position: relative;
  top: 0;
  left: -54%;
  transform: translate(54%, 0) !important;
  width: 480px !important;
  height: auto !important;
}

// Text
.text {
  width: 100%;
  margin-top: 2em !important;
  position: relative;
  top: 0%;
  left: 0%;
  transform: translate(0%, 0%) !important;
  text-align: center !important;
  }

  .h {
  font-size: 2.5rem;
  color: $v-dark-blue;
  line-height: 1.2 !important;
  margin-bottom: 0.2em !important;
}

.t-br-1 {
  display: none;
}

.t-br-2 {
  display: block;
}

.b {
  font-size: 16px;
}

.m-bg {
  background-image: url(../assets/bg-shorten-mobile.svg) !important;
}

.mid {
  height: 10em;
}

.u-s-div {
  position: absolute;
  top: 50%;
  left: 0%;
  transform: translate(0%, -50%) !important;
  z-index: 1 !important;
}

// Input
.u-s-i {
  width: 14em !important;
  height: auto;
  padding: 0.6em 0 0.6em 1em !important;
}

// Shorten It Btn
.s {
  margin-top: 1em !important;
  width: 15em;
  height: auto;
  padding: 0.6em 0 0.6em 0em !important;
  }

// Shorten It Btn
.s {
  margin-top: 1.5em !important;
  width: 15em;
  height: auto;
  padding: 0.6em 2em 0.6em 2em !important;
  }

  // Shortened Links
  .s-links-bg {
    height: 10em !important;
  }

  .sh-links {
  position: relative;
  margin-left: 1.2em !important;
  }

  // Copy Btn
.cy-bg {
  position: relative;
  top: 0%;
  right: 0% !important;
  transform: translate(0%, 0%) !important;
  margin-top: 1em !important;
  margin-left: 1.2em !important;
  margin-right: 1.2em !important;
}

.cy {
  width: 15em;
  height: auto;
  padding: 0.6em 2em 0.6em 2em !important;
}

.h-2 {
  font-size: 1.65em !important;
  padding-top: 0.5em !important;
}

.t-2-br-1 {
  display: none;
}

.b-2 {
  font-size: 16px !important;
  padding-left: 3em !important;
  padding-right: 3em !important;
}

  // Features
.f {
  margin-top: 25% !important;
}

.f-1, .f-2, .f-3 {
  width: 70%;
  height: auto;
  background: #fff;
  margin-left: 0em !important;
  z-index: 1 !important;
}

.f-1 {
  margin: 0 auto !important;
}

.f-2 {
  margin: 25% auto 0 auto !important;
}

.f-3 {
  margin: 25% auto 0 auto !important;
}

.i-bg {
  margin-top: -25% !important;
  }

  .b-bg {
    background-image: url(../assets/bg-boost-mobile.svg);
  }

  .b-text {
    font-size: 1.5em !important;
  }
}

// 375px
@media screen and (max-width: 375px) {
// Illustration
.i-w {
  position: relative;
  top: 0;
  left: -30%;
  transform: translate(30%, 0) !important;
  width: 480px !important;
  height: auto !important;
}

// Text
.text {
  width: 100%;
  margin-top: 2em !important;
  position: relative;
  top: 0%;
  left: 0%;
  transform: translate(0%, 0%) !important;
  text-align: center !important;
  }

  .h {
  font-size: 2.5rem;
  color: $v-dark-blue;
  line-height: 1.2 !important;
  margin-bottom: 0.2em !important;
}

.t-br-1 {
  display: none;
}

.b {
  font-size: 16px;
}

.m-bg {
  background-image: url(../assets/bg-shorten-mobile.svg) !important;
}

.u-s-div {
  position: absolute;
  top: 50%;
  left: 0%;
  transform: translate(0%, -50%) !important;
  z-index: 1 !important;
}

// Input
.u-s-i {
  width: 12em !important;
  height: auto;
  padding: 0.6em 0 0.6em 1em !important;
}

// Shorten It Btn
.s {
  margin-top: 1em !important;
  width: 13em;
  height: auto;
  padding: 0.6em 0 0.6em 0em !important;
  }

  .sh-links {
  margin-left: 1.2em !important;
  }

  // Copy Btn
  .cy-bg {
  margin-left: 1.2em !important;
  margin-right: 1.2em !important;
}

  .cy {
  width: 13.2em;
  height: auto;
  padding: 0.6em 2em 0.6em 2em !important;
}

.a-sh-links-2 {
  margin-left: 1.8em !important;
}

.h-2 {
  font-size: 1.65em !important;
  padding-top: 0.5em !important;
}

.t-2-br-1 {
  display: none;
}

.b-2 {
  font-size: 16px !important;
  padding-left: 1em !important;
  padding-right: 1em !important;
}

  // Features
.f {
  margin-top: 25% !important;
}

.f-1, .f-2, .f-3 {
  width: 70%;
  height: auto;
  background: #fff;
  margin-left: 0em !important;
  z-index: 1 !important;
}

.f-1 {
  margin: 0 auto !important;
}

.f-2 {
  margin: 25% auto 0 auto !important;
}

.f-3 {
  margin: 25% auto 0 auto !important;
}

.i-bg {
  margin-top: -25% !important;
  }

  .b-bg {
    background-image: url(../assets/bg-boost-mobile.svg);
  }

  .b-text {
    font-size: 1.5em !important;
  }
}

// 360px
@media screen and (max-width: 360px) {
.u-s-div {
  position: absolute;
  top: 50%;
  left: -20%;
  transform: translate(20%, -50%) !important;
  z-index: 1 !important;
  }

  .cy {
  width: 12.9em;
  }
}

// 320px
@media screen and (max-width: 320px) {
  .inner {
    display: none;
  }

  .n-res {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) !important;
  display: block;
  width: 50%;
  height: auto;
  padding: 1em !important;
  background: rgb(226, 64, 64);
  border-radius: 6px;
}

.n-res-h {
  color: #fff;
  text-align: center;
  }
}
</style>
