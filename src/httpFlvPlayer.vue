<template>
  <div class="video-player">
    <video :id="id" v-show="!loading">
    </video>
    <div class="loading" v-if="loading">
      <img src="@/assets/images/svg-loaders/three-dots.svg" width="64" alt="">
      <span class="tips">加载中...</span>
    </div>
    <div class="player-tools-box">
      <div class="content">
        <!-- <span @click="screenshotDownload">
        <svg t="1580638582687" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg"
             p-id="3459" width="16" height="16">
          <path d="M835.3 250.9v522.3H188.7V250.9h646.6m49.8-49.8H138.9v621.8H885V201.1h0.1z" p-id="3460"
                fill="#ffffff"></path>
          <path
            d="M138.9 101.6v99.5H64.3v49.8H188.7V101.6zM885.1 922.4v-99.5h74.6v-49.8H835.3v149.3zM511 705.4H297.5c-7.8 0-20.4-2.9-23.3-7.8-2.9-4.9 1.9-16.5 5.8-23.3 26.2-39.8 53.4-79.6 79.6-119.4 8.7-12.6 17.5-13.6 31.1-7.8 44.6 21.4 90.3 42.7 135.9 64.1 12.6 5.8 28.1 1.9 35.9-9.7 24.3-37.9 49.5-74.7 75.7-111.6 4.9-6.8 13.6-17.5 20.4-17.5 7.8 0 13.6 12.6 16.5 20.4 24.3 60.2 47.6 121.3 70.9 181.5 9.7 25.2 5.8 31.1-23.3 31.1H511z m-78.6-298c0 29.1-25.2 52.4-54.4 51.4-29.1-1-51.4-23.3-51.4-51.4 0-29.1 24.3-52.4 54.4-51.4 27.1 0.9 51.4 24.2 51.4 51.4z"
            p-id="3461" fill="#ffffff"></path>
        </svg>
        </span> -->
        <span @click="play" v-if="!playStatus">
        <svg t="1580638346729" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg"
             p-id="3031" width="16" height="16">
          <path
                  d="M512 0A512 512 0 1 0 1024 512 512.589353 512.589353 0 0 0 512 0z m0 965.064748A453.064748 453.064748 0 1 1 965.064748 512 453.580432 453.580432 0 0 1 512 965.064748z"
                  fill="#ffffff" p-id="3032"></path>
          <path
                  d="M735.953957 488.425899l-294.676259-221.007194a29.467626 29.467626 0 0 0-47.148202 23.574101v442.014388a29.467626 29.467626 0 0 0 47.148202 23.574101l294.676259-221.007194a29.467626 29.467626 0 0 0 0-47.148202zM453.064748 674.071942v-324.143884l216.071367 162.071942z"
                  fill="#ffffff" p-id="3033"></path>
        </svg>
        </span>
        <span @click="pause" v-if="playStatus">
        <svg t="1580646438705" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg"
             p-id="2132" width="16" height="16"><path
                d="M512.449956 124.087882c52.394883 0 103.189923 10.298994 150.985255 30.497022 46.195489 19.498096 87.691436 47.495362 123.287961 83.191876 35.696514 35.696514 63.59379 77.192462 83.191875 123.28796 20.198028 47.795332 30.497022 98.590372 30.497022 150.985255s-10.298994 103.189923-30.497022 150.985255c-19.498096 46.195489-47.495362 87.691436-83.191875 123.287961-35.696514 35.696514-77.192462 63.59379-123.287961 83.191875-47.795332 20.198028-98.590372 30.497022-150.985255 30.497022s-103.189923-10.298994-150.985255-30.497022c-46.195489-19.498096-87.691436-47.495362-123.28796-83.191875-35.696514-35.696514-63.59379-77.192462-83.191876-123.287961-20.198028-47.795332-30.497022-98.590372-30.497022-150.985255s10.298994-103.189923 30.497022-150.985255c19.498096-46.195489 47.495362-87.691436 83.191876-123.28796 35.696514-35.696514 77.192462-63.59379 123.28796-83.191876 47.795332-20.198028 98.590372-30.497022 150.985255-30.497022m0-59.994141c-247.375842 0-447.956254 200.580412-447.956254 447.956254s200.580412 447.956254 447.956254 447.956254 447.956254-200.580412 447.956254-447.956254-200.580412-447.956254-447.956254-447.956254z"
                p-id="2133" fill="#ffffff"></path><path
                d="M432.457768 322.068548c-16.598379 0-29.997071 13.398692-29.997071 29.997071v319.968753c0 16.598379 13.398692 29.997071 29.997071 29.99707s29.997071-13.398692 29.99707-29.99707v-319.968753c0-16.498389-13.398692-29.997071-29.99707-29.997071zM592.442144 322.068548c-16.598379 0-29.997071 13.398692-29.99707 29.997071v319.968753c0 16.598379 13.398692 29.997071 29.99707 29.99707s29.997071-13.398692 29.997071-29.99707v-319.968753c0-16.498389-13.398692-29.997071-29.997071-29.997071z"
                p-id="2134" fill="#ffffff"></path></svg>
        </span>
        <!--  <svg t="1580638188131" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg"
               p-id="1905" width="16" height="16">
            <path
              d="M856.573 512l89.179 89.179a31.53 31.53 0 1 1-44.589 44.589l-89.178-89.18-89.18 89.179a31.53 31.53 0 1 1-44.589-44.589L767.395 512l-89.179-89.18a31.53 31.53 0 1 1 44.589-44.589l89.18 89.179 89.179-89.179a31.53 31.53 0 1 1 44.589 44.589zM566.985 953h-2a41.806 41.806 0 0 1-25.786-8.86c0.013 0.124 0.017 0.249 0.031 0.373L264.44 743H118.985a50 50 0 0 1-50-50V333a50 50 0 0 1 50-50h142.727L539.23 79.487c-0.014 0.123-0.018 0.249-0.031 0.372A41.808 41.808 0 0 1 564.985 71h2a42 42 0 0 1 42 42v2c0 0.1-0.007 0.2-0.008 0.3h0.008v793.4l-0.008-0.006c0 0.1 0.008 0.2 0.008 0.3v2a42 42 0 0 1-42 42.006z m-358-595a15 15 0 0 0-15-15h-50a15 15 0 0 0-15 15v310a15 15 0 0 0 15 15h50a15 15 0 0 0 15-15V358z m340-167.7c-0.051 0.063-0.111 0.119-0.163 0.181a19.991 19.991 0 0 0-33.656-11.934L283.985 335c-0.087 0-0.17 0.011-0.256 0.013 0.053 0.133 0.091 0.273 0.141 0.407a32.988 32.988 0 0 0-14.621 23.469c-0.089 0.009-0.175 0.028-0.264 0.035v306.152c0.089 0.007 0.175 0.026 0.264 0.035a32.988 32.988 0 0 0 14.621 23.469c-0.05 0.134-0.088 0.274-0.141 0.407 0.086 0 0.169 0.013 0.256 0.013l231.181 156.451a19.991 19.991 0 0 0 33.656-11.934c0.052 0.062 0.112 0.118 0.163 0.181V190.3z"
              fill="#ffffff" p-id="1906"></path>
          </svg>-->
        <span @click="fullscreen(`#${id}`)">
        <svg t="1580638612623" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg"
             p-id="4329" width="16" height="16">
          <path
                  d="M664.035 409.382l244.223-243.378-0.837 137.922c-0.335 11.437 8.912 21.527 20.351 21.191h14.63c11.438-0.335 21.025-7.065 21.193-18.67l0.672-205.367c0-0.171 0.335-10.934 0.335-10.934 0.17-5.716-1.179-10.934-4.879-14.63-3.7-3.702-8.742-6.055-14.633-5.886l-10.428 0.171c-0.169 0-0.331 0-0.501 0.171l-203.69-0.846c-11.438 0.336-21.025 9.76-21.193 21.361v14.633c1.685 13.625 12.446 21.529 23.884 21.193l134.219 0.335-243.551 242.542c-11.101 11.104-11.101 29.095 0 40.197 11.104 11.269 29.101 11.269 40.203 0h-0.003M356.233 638.806l-244.393 242.544 0.842-137.253c0.336-11.435-8.918-21.523-20.355-21.193h-15.47c-11.438 0.335-21.025 7.065-21.193 18.672l-0.672 205.536c0 0.171-0.335 10.934-0.335 10.934-0.171 5.722 1.18 10.934 4.875 14.63 3.7 3.7 8.746 6.055 14.633 5.886l10.427-0.17c0.171 0 0.336 0 0.507-0.171l204.532 0.843c11.435-0.336 21.025-9.756 21.193-21.361v-14.63c-1.683-13.625-12.451-21.529-23.887-21.193l-134.222-0.335 243.38-242.539c11.104-11.104 11.104-29.101 0-40.203-10.929-11.268-28.757-11.268-39.857 0.001v0M964.271 947.109l-0.507-205.536c-0.336-11.438-9.76-18.335-21.194-18.672h-14.629c-11.439-0.331-20.521 9.759-20.356 21.193l0.843 137.927-244.393-243.214c-11.104-11.104-29.099-11.104-40.203 0-11.097 11.101-11.097 29.099 0 40.203l243.386 242.538-134.22 0.335c-11.438-0.335-22.034 7.739-23.887 21.193v14.633c0.335 11.437 9.76 21.025 21.193 21.361l203.69-0.843c0.17 0 0.335 0.17 0.507 0.17l10.428 0.171c5.716 0.17 10.934-2.016 14.63-5.886 3.698-3.7 5.042-8.912 4.875-14.63 0 0-0.169-10.764-0.169-10.934l0.004-0.002M152.885 126.645l134.22-0.335c11.435 0.335 22.031-7.739 23.883-21.193v-14.636c-0.336-11.437-9.753-21.025-21.193-21.36l-204.694 0.842c-0.17 0-0.336-0.171-0.509-0.171l-10.426-0.169c-5.722-0.17-10.934 2.015-14.633 5.885-3.698 3.7-5.050 8.912-4.875 14.633 0 0 0.335 10.763 0.335 10.933l0.502 205.536c0.171 11.435 9.759 18.335 21.193 18.667h15.475c11.437 0.335 20.519-9.753 20.349-21.191l-0.671-137.248 244.224 242.709c11.097 11.104 29.094 11.104 40.196 0 11.104-11.101 11.104-29.099 0-40.203l-243.38-242.703M152.885 126.645v0z"
                  p-id="4330" fill="#ffffff"></path>
        </svg>
        </span>
      </div>
    </div>
  </div>

</template>

<script>
  import flvjs from 'flv.js'

  export default {
    name: 'httpFlvPlayer',
    props: {
      id: {
        type: String,
        default: 'flv-player'
      },
      src: {
        type: String,
        default: ''
      }
    },
    data() {
      return {
        playStatus: true,
        flvPlayer: null,
        prefixName: '',
        loading: false,
        errCount: 0
      }
    },
    methods: {
      screenshot() {
        let videoElement = document.getElementById(`${this.id}`)
        let canvas = document.createElement('canvas')
        canvas.width = videoElement.videoWidth
        canvas.height = videoElement.videoHeight
        canvas.getContext('2d').drawImage(videoElement, 0, 0, canvas.width, canvas.height)
        let url = canvas.toDataURL('image/png')
        console.log(url)
        return url
      },
      screenshotDownload() {
        var a = document.createElement('a')
        a.href = this.screenshot()
        a.download = name
        a.click()
      },
      play() {
        this.playStatus = true
        this.flvPlayer.play()
      },
      stop() {
        console.log(this.flvPlayer)
        if (this.flvPlayer) {
          // this.flvPlayer.pause()
          this.flvPlayer.unload()
          // 卸载DOM对象
          this.flvPlayer.detachMediaElement()
          // 销毁flvjs对象
          this.flvPlayer.destroy()
        }
      },
      pause() {
        this.playStatus = false
        this.flvPlayer.pause()
      },
      isFullscreen(fn) {
        let fullscreenEnabled
        // 判断浏览器前缀
        if (document.fullscreenEnabled) {
          fullscreenEnabled = document.fullscreenEnabled
        } else if (document.webkitFullscreenEnabled) {
          fullscreenEnabled = document.webkitFullscreenEnabled
          this.prefixName = 'webkit'
        } else if (document.mozFullScreenEnabled) {
          fullscreenEnabled = document.mozFullScreenEnabled
          this.prefixName = 'moz'
        } else if (document.msFullscreenEnabled) {
          fullscreenEnabled = document.msFullscreenEnabled
          this.prefixName = 'ms'
        }
        if (!fullscreenEnabled) {
          if (fn !== undefined) fn() // 执行不支持全屏的回调
          this.isFullscreenData = false
        }
      },
      fullscreen(domName) {
        let fullscreenStatus = window.localStorage.getItem('fullscreenStatus')
        if (!!fullscreenStatus) {
          const methodName =
                  this.prefixName === ''
                          ? 'exitFullscreen'
                          : `${this.prefixName}ExitFullscreen` // API 前缀
          document[methodName]() // 调用
          window.localStorage.removeItem('fullscreenStatus')
        } else {
          window.localStorage.setItem('fullscreenStatus', 1)
          this.isFullscreen()
          const element = document.querySelector(domName) // 获取dom
          const methodName =
                  this.prefixName === ''
                          ? 'requestFullscreen'
                          : `${this.prefixName}RequestFullScreen` // API前缀
          element[methodName]() // 调用全屏
        }
      },
      createPlayer() {
        let _this = this
        if (this.flvPlayer) {
          return
        }
        if (flvjs.isSupported()) {
          let source = {
            isLive: true,
            hasAudio: false,
            type: 'flv',
            url: this.src,
            enableStashBuffer: false,
            autoCleanupSourceBuffer: true,
            autoCleanupMaxBackwardDuration: 5,
            autoCleanupMinBackwardDuration: 1,
            stashInitialSize: 32
          }
          this.flvPlayer = flvjs.createPlayer(source)

          this.flvPlayer.attachMediaElement(document.getElementById(this.id))
          this.flvPlayer.on(flvjs.Events.ERROR, (errorType, errorDetail, errorInfo) => {
                    console.log('errorType:', errorType)
                    console.log('errorDetail:', errorDetail)
                    console.log('errorInfo:', errorInfo)
                    // 如果视频播放出错就销毁player，用当前的url重新创建一个
                    if (_this.flvPlayer) {
                      _this.stop()
                      if (_this.errCount < 2) {
                        _this.createPlayer()
                      }
                    }
                  }
          )
          this.flvPlayer.on(flvjs.Events.MEDIA_INFO, (data) => {
                    //console.log(data)
                  }
          )
          this.flvPlayer.on(flvjs.Events.STATISTICS_INFO, (data) => {
                    // console.log(data)
                    if (data.speed == 0) {
                      _this.loading = true
                    } else {
                      setTimeout(function() {
                        _this.loading = false
                      }, 1000)
                    }
                  }
          )

          this.flvPlayer.on(flvjs.Events.LOADING_COMPLETE, function() {
            console.log('断流了')
          })
          this.flvPlayer.load()
          const playPromise = this.flvPlayer.play()
          playPromise.catch((error) => {
            console.log('Catch error: ', error)
          })
        }
      }
    },
    mounted() {
      this.createPlayer()
    },
    destroyed() {
      if (this.flvPlayer) {
        this.stop()
      }
    },
    watch: {
      src: {
        handler: function(newVal, oldVal) {
          let _this = this
          console.log(newVal)
          if (newVal != oldVal) {
            if (_this.flvPlayer) {
              _this.stop()
            }
          }
          if (newVal) {
            _this.createPlayer()
          }
        }
      }
    }
  }
</script>

<style lang="less" scoped>
  .video-player {
    overflow: hidden;
    color: #ffffff;
    height: 100%;
    width: 100%;
    background: #003A55;
    text-align: center;
    vertical-align: middle;

    //border-left: 1px #5d6c7b solid;
    //border-bottom: 1px #5d6c7b solid;

    video {
      height: 100%;
      width: 100%;
      z-index: 1;
    }

    .loading {
      z-index: 999;
      position: relative;
      opacity: 0.5;
      height: 100%;
      width: 100%;
      display: flex;
      justify-content: center; /* 水平居中 */
      align-items: center; /* 垂直居中 */
      flex-direction: column;

      image {
        z-index: 999;
      }

      span {
        z-index: 999;
        margin-top: 5px;
        display: block;
        font-size: 11px;
      }
    }

    .player-tools-box {
      padding: 3px;
      height: 28px;
      line-height: 22px;
      background: #8c939d;
      opacity: 0.8;
      width: 100%;

      .content {
        float: right;
        margin-right: 10px;

        svg {
          cursor: pointer;
          margin-left: 5px;
        }
      }
    }
  }

  .video-player:hover {
    .player-tools-box {
      margin-top: -28px;
    }
  }
</style>
