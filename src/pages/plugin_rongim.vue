<template>
    <div class="app">

        <navbar class="navbar">
            <navbar-item type="back"></navbar-item>
            <navbar-item type="title">
                <text class="title">{{lang("融云通信模块")}}</text>
            </navbar-item>
            <navbar-item type="right" @click="viewCode('markets/eeui/rongim')">
                <icon content="md-code-working" class="iconr"></icon>
            </navbar-item>
        </navbar>

        <div class="content">

            <text class="info">{{info}}</text>
            <text class="button" @click="login">{{lang("连接登录")}}</text>

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

    .info {
        font-size: 22px;
        margin-bottom: 20px
    }

    .button {
        font-size: 24px;
        text-align: center;
        margin-top: 20px;
        padding-top: 20px;
        padding-bottom: 20px;
        width: 220px;
        color: #ffffff;
        background-color: #00B4FF;
    }
</style>

<script>
    const eeui = app.requireModule('eeui');
    const rongim = app.requireModule('eeui/rongim');

    require("../i18n");

    export default {
        data() {
            return {
                info: '',
            }
        },
        created() {
            this.addLanguageData("en", {
                "连接登录": "Connect Login",
                "测试会员": "test user",
                "检测到未安装rongim插件，安装详细请登录https://eeui.app/": "No installation of the rongim plug-in, please login https://eeui.app/ for installation details",
            });
        },
        methods: {
            viewCode(str) {
                this.openViewCode(str);
            },

            login() {
                if (typeof rongim === 'undefined') {
                    eeui.alert({
                        title: this.lang('温馨提示'),
                        message: this.lang("检测到未安装rongim插件，安装详细请登录https://eeui.app/"),
                    });
                    return;
                }
                eeui.loading();
                rongim.login({
                    userid: 'eeui_' + WXEnvironment.platform,
                    username: this.lang('测试会员'),
                    userimg: 'https://www.baidu.com/img/baidu_resultlogo@2.png',
                }, (result) => {
                    eeui.loadingClose();
                    this.info = result;
                });
            }
        }
    };
</script>
