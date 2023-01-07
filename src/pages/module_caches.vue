<template>
    <div class="app">

        <navbar class="navbar">
            <navbar-item type="back"></navbar-item>
            <navbar-item type="title">
                <text class="title">{{lang("数据缓存")}}</text>
            </navbar-item>
            <navbar-item type="right" @click="viewCode('module/caches')">
                <icon content="md-code-working" class="iconr"></icon>
            </navbar-item>
        </navbar>

        <div class="content">

            <text class="subtitle">{{lang("数据缓存：重启APP不被删除")}}</text>

            <text style="font-size:24px">{{caches}}</text>

            <text class="button" @click="setCaches()">{{lang("设置缓存")}}</text>
            <text class="button" @click="getCaches()">{{lang("读取缓存")}}</text>


            <text class="subtitle">{{lang("全局变量：重启APP后数据不存在")}}</text>

            <text style="font-size:24px">{{variate}}</text>

            <text class="button" @click="setVariate()">{{lang("设置变量")}}</text>
            <text class="button" @click="getVariate()">{{lang("读取变量")}}</text>

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
        align-items: center;
    }

    .subtitle {
        padding-top: 56px;
        padding-right: 24px;
        padding-bottom: 24px;
        padding-left: 24px;
        font-size: 28px;
        color: #757575;
    }

    .button {
        width: 380px;
        font-size: 24px;
        text-align: center;
        margin-top: 20px;
        margin-bottom: 20px;
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
        data() {
            return {
                caches: '',
                variate: '',
            }
        },

        created() {
            this.addLanguageData("en", {
                "数据缓存：重启APP不被删除": "Cache: restart APP will not be deleted",
                "设置缓存": "Set cache",
                "读取缓存": "Get cache",
                "全局变量：重启APP后数据不存在": "Variable: data does not exist after restarting the APP",
                "设置变量": "Set variable",
                "读取变量": "Get variable",
                "读取成功，缓存：": "Cache: ",
                "读取成功，变量：": "Variable: ",
            });
        },

        mounted() {
            this.caches = eeui.getCachesString('tempName', '');
            this.variate = eeui.getVariate('tempName', '');
        },

        methods: {
            viewCode(str) {
                this.openViewCode(str);
            },
            randomString(len) {
                len = len || 32;
                let $chars = 'ABCDEFGHJKMNPQRSTWXYZabcdefhijkmnprstwxyz2345678oOLl9gqVvUuI1';
                let maxPos = $chars.length;
                let pwd = '';
                for (let i = 0; i < len; i++) {
                    pwd += $chars.charAt(Math.floor(Math.random() * maxPos));
                }
                return pwd;
            },

            setCaches() {
                this.caches = this.randomString(16);
                eeui.setCachesString('tempName', this.caches, 0);
            },
            getCaches() {
                this.caches = eeui.getCachesString('tempName', '');
                eeui.toast(this.lang("读取成功，缓存：") + this.caches)
            },

            setVariate() {
                this.variate = this.randomString(16);
                eeui.setVariate('tempName', this.variate);
            },
            getVariate() {
                this.variate = eeui.getVariate('tempName', '');
                eeui.toast(this.lang("读取成功，变量：") + this.variate)
            },
        }
    };
</script>
