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
          <a :href="link" target="_blank" class="a-sh-links-2">{{ link }}</a>
          </li>
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
@import "../styles/url-shortener.scss";
</style>
