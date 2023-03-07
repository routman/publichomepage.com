<template>
  <div id="main">
    <a href="https://publichomepage.com" id="logo">
      <div class="title accent">public</div><div class="title">homepage</div>
    </a>
    
    <router-view class="page"/>
    
    <nav id="nav">
      <router-link class="menu link" to="/about" v-if="!isAbout">about</router-link>
      <router-link class="menu link" to="/" v-if="isAbout">home</router-link>
      <a class="menu link" href="https://publicnote.com" target="_blank" rel="noopener">publicnote</a>
    </nav>
    
  </div>
</template>

<script>
export default {
    computed: {
        isAbout() {
            return this.$route.name == 'about'
        }
    }
}
</script>

<style lang="scss">
@import "assets/settings.scss";
html, body {
  font-family: $font;
  font-size: 18px;
  font-weight: 500;
  color: $color-text;
  background: $color-bg;
  margin: 0;
  width: 100%;
  height: 100%;
}

#app {
  display: flex;
  flex-grow: 1;
  flex-direction: column;
  justify-content: space-between;
  padding: $app-margin;
  height: calc(100% - (2*$app-margin));
}

#main {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  height: 100%;
}

.page {
  flex-grow: 1;
  overflow-y: scroll;
  -ms-overflow-style: none;
  scrollbar-width: none;
  -webkit-overflow-scrolling: touch;
  display: flex;
  flex-direction: column;
}
.page::-webkit-scrollbar {
  display: none;
}

.title {
  display: inline-block;
  flex-grow: 0;
  font-size: 22px;
  letter-spacing: 3px;
  color: $color-text;
}

.accent {
  color: $color-primary !important;
  margin-right: 4px;
}

.subtitle {
  flex-grow: 0;
  margin-bottom: 12px;
  line-height: 40px;
}

#nav {
  flex-grow: 0;
  padding-top: 12px;
}

#logo {
  flex-grow: 0;
}

.link {
  text-decoration: none;
  color: $color-primary;
}

.menu { 
  margin-right: 40px;
}

input::selection {
  background: $color-selection;
}
textarea::selection {
  background: $color-selection;
}

input, textarea {
  display: block;
  font-family: $font;
  caret-color: $color-primary;
  background: $color-bg;
  font-size: 18px;
  border: none;
  border-radius: 0;
  box-sizing: border-box;
}
input:focus, textarea:focus {
  outline: none;
  border: none;
}
input {
  flex-grow: 0;
  line-height: 40px;
  margin: 0 0 12px 0;
  padding: 0;
}

textarea {
  flex-grow: 1;
  width: 100%;
  padding: 0;
  line-height: 20px;
  overflow-y: scroll;
  -ms-overflow-style: none;
  scrollbar-width: none;
  -webkit-overflow-scrolling: touch;
}
textarea::-webkit-scrollbar {
  display: none;
}

@media (prefers-color-scheme: dark) {
  html, body {
    color: $color-text-dark;
    background: $color-bg-dark;
  }

  input, textarea {
    color: $color-text-dark;
    background: $color-bg-dark;
    caret-color: $color-primary-dark;
  }

  .link {
    color: $color-primary-dark;
  }
  .title {
    color: $color-text-dark;
  }

  .eye.icon {
    color: $color-primary-dark;
  }
  .eye.icon:before {
    border: solid 2px $color-primary-dark;
  }
  .closedeye.icon {
    color: $color-primary-dark;
  }
  .closedeye.icon:before {
    border: solid 2px $color-primary-dark;
  }
  
}

</style>

