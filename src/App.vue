<template>
  <div id="app">
    <router-view />
    <!-- <div class="loading" v-if="isshow">
      <div class="icons"></div>
    </div>
    <transition name="fade">
      <router-view v-if="!isshow" />
    </transition> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      isshow: true
    }
  },
  computed: {
    isPC() {
      if (
        navigator.userAgent.match(
          /(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i
        )
      ) {
        return false
      } else {
        return true
      }
    }
  },
  mounted() {
    if (this.isPC) {
      setTimeout(() => {
        this.isshow = false
      }, 1500)
    } else {
      this.isshow = false
    }
    ;(function(doc, win) {
      var docEl = doc.documentElement,
        resizeEvt =
          'orientationchange' in window ? 'orientationchange' : 'resize',
        recalc = function() {
          var clientWidth = docEl.clientWidth > 750 ? 750 : docEl.clientWidth

          if (!clientWidth) {
            return
          }

          docEl.style.fontSize = 100 * (clientWidth / 750) + 'px'
        }

      recalc()

      if (!doc.addEventListener) return

      win.addEventListener(resizeEvt, recalc, false)

      doc.addEventListener('DOMContentLoaded', recalc, false)
    })(document, window)
  }
}
</script>

<style lang="less">
html {
  background: #fff;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  .loading {
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    .icons {
      width: 80px;
      height: 80px;
      background: url(./assets/images/loading.svg) no-repeat;
      background-size: contain;
      animation: spin ease-in-out 1.5s 10;
      transform-origin: center;
    }
  }
}
@-webkit-keyframes spin {
  from {
    -webkit-transform: rotate(0deg);
  }
  to {
    -webkit-transform: rotate(360deg);
  }
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
.fade-enter-active {
  transition: opacity 0.2s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
