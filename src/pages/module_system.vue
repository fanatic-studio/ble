<template>
    <div class="app">

        <navbar class="navbar">
            <navbar-item type="back"></navbar-item>
            <navbar-item type="title">
                <text class="title">{{lang("系统信息")}}</text>
            </navbar-item>
            <navbar-item type="right" @click="viewCode('module/system')">
                <icon content="md-code-working" class="iconr"></icon>
            </navbar-item>
        </navbar>

        <div class="content">
            <text class="item" v-for="(item, index) in lists" :key="index">{{item}}</text>
        </div>

    </div>
</template>

<style>
    .app {
        width: 750px;
        flex: 1;
    }

    .navbar {
        width: 750px;
        height: 100px;
    }

    .title {
        font-size: 28px;
        color: #ffffff
    }

    .iconr {
        width: 100px;
        height: 100px;
        color: #ffffff;
    }

    .content {
        flex: 1;
    }

    .item {
        padding-top: 26px;
        padding-bottom: 26px;
        padding-left: 30px;
        padding-right: 30px;
        font-size: 24px;
    }
</style>

<script>
    const eeui = app.requireModule('eeui');

    require("../i18n");

    export default {
        data() {
            return {
                lists: [],
            }
        },

        created() {
            this.addLanguageData("en", {
                "获取状态栏高度（屏幕像素）：": "Get the height of the status bar (screen pixels) : ",
                "获取状态栏高度（px单位）：": "Gets the height of the status bar (px unit) : ",
                "获取虚拟键盘高度（屏幕像素）：": "Get virtual keyboard height (screen pixels) : ",
                "获取虚拟键盘高度（px单位）：": "Get virtual keyboard height (px unit) : ",
                "获取本地软件版本号：": "Get local software version number: ",
                "获取本地软件版本号名称：": "Get local software version number name: ",
                "获取手机的IFA：": "Obtain the IFA of the phone: ",
                "获取手机的IMEI：": "Obtain the IMEI of the phone: ",
                "获取设备系统版本号：": "Get device system version number: ",
                "获取设备系统版本名称：": "Get device system version name: ",
            });
        },

        mounted() {
            this.lists.push(this.lang("获取状态栏高度（屏幕像素）：") + eeui.getStatusBarHeight());
            this.lists.push(this.lang("获取状态栏高度（px单位）：") + eeui.getStatusBarHeightPx());
            this.lists.push(this.lang("获取虚拟键盘高度（屏幕像素）：") + eeui.getNavigationBarHeight());
            this.lists.push(this.lang("获取虚拟键盘高度（px单位）：") + eeui.getNavigationBarHeightPx());
            this.lists.push(this.lang("获取本地软件版本号：") + eeui.getLocalVersion());
            this.lists.push(this.lang("获取本地软件版本号名称：") + eeui.getLocalVersionName());
            if (/ios/i.test(WXEnvironment.platform)) {
                this.lists.push(this.lang("获取手机的IFA：") + eeui.getIfa());
            }else{
                this.lists.push(this.lang("获取手机的IMEI：") + eeui.getImei());
            }
            this.lists.push(this.lang("获取设备系统版本号：") + eeui.getSDKVersionCode());
            this.lists.push(this.lang("获取设备系统版本名称：") + eeui.getSDKVersionName());
        },

        methods: {
            viewCode(str) {
                this.openViewCode(str);
            },
        }
    };
</script>
