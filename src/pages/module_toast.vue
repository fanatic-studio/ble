<template>
    <div class="app">

        <navbar class="navbar">
            <navbar-item type="back"></navbar-item>
            <navbar-item type="title">
                <text class="title">{{lang("提示消息")}}</text>
            </navbar-item>
            <navbar-item type="right" @click="viewCode('module/toast')">
                <icon content="md-code-working" class="iconr"></icon>
            </navbar-item>
        </navbar>

        <div class="content">
            <text class="button" @click="toast1">{{lang("普通的toast")}}</text>
            <text class="button" @click="toast2">{{lang("红色的toast")}}</text>
            <text class="button" @click="toast3">{{lang("背景红色的toast")}}</text>
            <text class="button" @click="toast4">{{lang("显示较长的toast")}}</text>
            <text class="button" @click="toast5">{{lang("顶部的toast")}}</text>
            <text class="button" @click="toast6">{{lang("中间的toast")}}</text>
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
        justify-content: center;
        align-items: center;
    }

    .button {
        width: 380px;
        font-size: 24px;
        text-align: center;
        margin-top: 15px;
        margin-bottom: 15px;
        padding-top: 26px;
        padding-bottom: 26px;
        padding-left: 30px;
        padding-right: 30px;
        color: #ffffff;
        background-color: #00B4FF;
    }
</style>

<script>
    const eeui = app.requireModule('eeui');

    require("../i18n");

    export default {
        created() {
            this.addLanguageData("en", {
                "普通的toast": "Normal toast",
                "红色的toast": "Red toast",
                "背景红色的toast": "Red background toast",
                "显示较长的toast": "Long toast",
                "顶部的toast": "Top toast",
                "中间的toast": "Middle toast",
            });
        },
        methods: {
            viewCode(str) {
                this.openViewCode(str);
            },
            toast1() {
                eeui.toast(this.lang("普通的toast"));
            },
            toast2() {
                eeui.toast({
                    message: this.lang('红色的toast'),
                    messageColor: '#ff0000'
                });
            },
            toast3() {
                eeui.toast({
                    message: this.lang('背景红色的toast'),
                    messageColor: '#ffffff',
                    backgroundColor: '#ff0000'
                });
            },
            toast4() {
                eeui.toast({
                    message: this.lang('显示较长的toast'),
                    long: true
                });
            },
            toast5() {
                eeui.toast({
                    message: this.lang('顶部的toast'),
                    gravity: 'top',
                    y: 50
                });
            },
            toast6() {
                eeui.toast({
                    message: this.lang('中间的toast'),
                    gravity: 'middle',
                });
            },
        }
    };
</script>
