<template>
  <div id="status">
    <div v-if="this.status == 'busy'" id="spinner"></div>
    <div v-if="this.status == 'ok'" id="checkmark"></div>
    <div v-if="this.status == 'error'" class="close icon"></div>
  </div>
  <input v-model="this.contents.subtitle" placeholder="enter subtitle here" v-on:keyup="saveSubtitle()" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false">
  <textarea v-model="this.contents.main" v-on:keyup="saveMain()" placeholder="enter main contents here"></textarea>
</template>

<script>
window.Filter = require('bad-words');

export default {
  name: 'home',
  data: function() {
    return {
      contents: {
        main: '',
        subtitle: '',
      },
      status: '',
      subautosave: null,
      mainautosave: null
    }
  },
  methods: {
    saveSubtitle: function() {
      var filter = new Filter();
      this.status = 'busy';
      this.contents.subtitle = this.contents.subtitle.substring(0,40);
      clearTimeout(this.subautosave);
      this.subautosave = setTimeout( () => {
        this.contents.subtitle = filter.clean(this.contents.subtitle);
        var d = {
          "subtitle": this.contents.subtitle
        };
        fetch('https://publichomepage.com/api/save', {
          method: 'POST',
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(d)
        })
        .then(response => {
          this.status = 'ok';
        },
        error => {
          console.log(error);
          this.status = 'error';
        });
        this.subautosave = null;
      }, 2000);
    },
    saveMain: function() {
      var filter = new Filter();
      this.status = 'busy';
      this.contents.main = this.contents.main.substring(0,8000);
      clearTimeout(this.mainautosave);
      this.mainautosave = setTimeout( () => {
        this.contents.main = filter.clean(this.contents.main);
        var d = {
          "main": this.contents.main,
        };
        fetch('https://publichomepage.com/api/save', {
          method: 'POST',
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(d)
        })
        .then(response => {
          this.status = 'ok';
        },
        error => {
          console.log(error);
          this.status = 'error';
        });
        this.mainautosave = null;
      }, 2000);
    }
  },
  mounted: function() {
    this.status = 'busy';
    fetch('https://publichomepage.com/api/get', {
      method: 'GET'
    })
    .then(data => data.json())
    .then(data => {
      this.contents = data;
      this.status = 'ok';
    },
    error => {
      console.log(error);
      this.status = 'error';
    });
  }
}
</script>

<style scoped lang="scss">
@import "../assets/settings.scss";

#status {
  position: absolute;
  top: 16px;
  left: 266px;
  user-select: none;
}

#spinner {
	display: inline-block;
  border: 2px solid;
  border-color: $color-inactive;
  border-top: 2px solid $color-bg;
  border-radius: 50%;
  width: 15px;
  height: 15px;
  animation: spin 0.5s linear infinite;
  margin-top: 12px;
  margin-right: 2px;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

#checkmark {
  display: inline-block;
  width: 8px;
  height: 16px;
  border: solid;
  border-color: $color-primary;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
  margin-top: 8px;
  margin-left: 3px;
}

.close.icon {
  display: inline-block;
  color: $color-alert;
  width: 21px;
  height: 21px;
  position: relative;
  margin-top: 4px;
}

.close.icon:before {
  content: '';
  position: absolute;
  top: 16px;
  width: 21px;
  height: 2px;
  background-color: currentColor;
  -webkit-transform: rotate(-45deg);
          transform: rotate(-45deg);
}
.close.icon:after {
  content: '';
  position: absolute;
  top: 16px;
  width: 21px;
  height: 2px;
  background-color: currentColor;
  -webkit-transform: rotate(45deg);
          transform: rotate(45deg);
}

@media (prefers-color-scheme: dark) {
  #spinner {
    border: 2px solid;
    border-color: $color-accent;
    border-top: 2px solid $color-bg-dark;
  }
  #checkmark {
    border-color: $color-primary-dark;
  }
}

</style>
