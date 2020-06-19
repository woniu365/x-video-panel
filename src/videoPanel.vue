<template>
    <div class="video-panel" :class="{'video-panel-mini':!isfullscreen,'video-panel-fullscreen':isfullscreen}">
        <div class="tools-box">
            <div class="tv_box" style="float: right;">
                <span @click="changeVideoBoxNum(1)"><i class="icon icon_num1"/></span>
                <span @click="changeVideoBoxNum(4)"><i class="icon icon_num2"/></span>
                <span @click="changeVideoBoxNum(6)"><i class="icon icon_num3"/></span>
                <span @click="changeVideoBoxNum(9)"><i class="icon icon_num5"/></span>
                <span @click="fullscreen('.video-panel')"><i class="icon icon_view"/></span>
                <!--            <span @click="startAllVideo"><i class="icon icon_play_all" title="预览所有视频"/></span>
                            <span @click="pauseAllVideo"><i class="icon icon_close_show"/></span>
                            <span><i class="icon icon_num9" title="参数设置"/></span>-->
            </div>
        </div>
        <div :class="'video-box '+videoBoxStyle">
            <div v-for="(item,index) in playVideoList" :key="'video-box-'+index"
                 class="video-box-list">
                <div class="no-source" v-if="!item.url">
                    <img src="./static/svg/video.svg" width="32" alt="">
                    <span class="tips">NO SOURCE</span>
                </div>
                <http-flv-player
                        :id="'flv-player-'+index"
                        ref="videoPlay"
                        :src="item.url"
                        v-if="item.url"
                        :loading="!item.url"
                />
            </div>
        </div>
    </div>
</template>

<script>
    import httpFlvPlayer from 'httpFlvPlayer'

    export default {
        components: {
            httpFlvPlayer
        },
        name: 'video-panel',
        data() {
            return {
                videoBoxStyle: 'vWin-1',
                isfullscreen: false,
                playVideoList: [
                    {
                        name: '',
                        url: ''
                    }
                ]
            }
        },
        created() {
            this.setVideoWindow(1)
        },
        methods:
            {
                startAllVideo() {
                    for (let i = 0; i < this.playVideoList.length; i++) {
                        this.$refs.videoPlay[i].play()
                    }
                },
                pauseAllVideo() {
                    for (let i = 0; i < this.playVideoList.length; i++) {
                        this.$refs.videoPlay[i].pause()
                    }
                },
                changeVideoBoxNum(num) {
                    window.localStorage.setItem('video_box_num', num)
                    this.setVideoWindow(num)
                },
                setVideoWindow(num) {
                    let arr = this.playVideoList
                    this.playVideoList = []
                    if (arr.length < num) {
                        let j = (num - arr.length)
                        for (let i = 0; i < j; i++) {
                            arr.push({name: '', url: ''})
                        }
                    } else {
                        arr = arr.slice(0, num)
                    }
                    this.playVideoList = arr
                    this.videoBoxNum = num
                    this.videoBoxStyle = 'vWin-' + num
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
                    }
                },
                fullscreen(domName) {
                    if (this.isfullscreen) {
                        const methodName =
                            this.prefixName === ''
                                ? 'exitFullscreen'
                                : `${this.prefixName}ExitFullscreen` // API 前缀
                        document[methodName]() // 调用

                        this.isfullscreen = false
                    } else {
                        this.isFullscreen()
                        this.isfullscreen = true
                        const element = document.querySelector(domName) // 获取dom
                        const methodName =
                            this.prefixName === ''
                                ? 'requestFullscreen'
                                : `${this.prefixName}RequestFullScreen` // API前缀
                        element[methodName]() // 调用全屏
                    }
                }
            }
    }
</script>


<style lang="less" scoped>

    //自定义覆盖面板尺寸
    @import './static/css/video_panel.less';

    .video-panel-mini {
        @vw: 29vw;
        @vh: @vw;

        .tools-box {
            width: @vw;
            min-width: @vw;
        }

        .video-box {
            background-color: @bgcolor;
            min-width: @min-width;
            min-height: calc(@min-width * 0.82);
            width: @vw;
            height: calc(@vw * 0.82);
        }
    }


    .el-checkbox__label {
        padding-left: 0px !important;
    }

    .el-checkbox {
        margin-right: 10px;
    }

    .el-select {
        width: 180px;
    }

    .label2 {
        vertical-align: middle;
        font-size: 14px;
        color: #606266;
        line-height: 40px;
        padding: 0 12px 0 0;
        -webkit-box-sizing: border-box;
        box-sizing: border-box;
        display: block;
    }

</style>
