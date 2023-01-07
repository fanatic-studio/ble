<template>
    <div class="app">

        <navbar class="navbar">
            <navbar-item type="back"></navbar-item>
            <navbar-item type="title">
                <text class="title">{{lang("弹窗验证")}}</text>
            </navbar-item>
            <navbar-item type="right" @click="viewCode('module/captcha')">
                <icon content="md-code-working" class="iconr"></icon>
            </navbar-item>
        </navbar>

        <div class="content">
            <text class="button" @click="swipeCaptcha">{{lang("开始验证")}}</text>
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

    require("../i18n");

    export default {
        created() {
            this.addLanguageData("en", {
                "开始验证": "validation",
                "验证成功": "validation successful",
                "验证失败": "validation fails",
            });
        },
        methods: {
            viewCode(str) {
                this.openViewCode(str);
            },
            swipeCaptcha() {
                eeui.swipeCaptcha(null, (res) => {
                    switch (res.status) {
                        case "success":
                            eeui.toast(this.lang("验证成功"));
                            break;

                        case "failed":
                            eeui.toast(this.lang("验证失败"));
                            break;
                    }
                });
            },
        }
    };
</script>
