<template>
    <div class="app">

        <navbar class="navbar">
            <navbar-item type="back"></navbar-item>
            <navbar-item type="title">
                <text class="title">{{lang("微信/支付宝支付")}}</text>
            </navbar-item>
            <navbar-item type="right" @click="viewCode('markets/eeui/pay')">
                <icon content="md-code-working" class="iconr"></icon>
            </navbar-item>
        </navbar>

        <div class="content">

            <text class="info">{{info}}</text>
            <text class="button" @click="weixinPay">{{lang("微信支付")}}</text>
            <text class="button" @click="alipayPay">{{lang("支付宝支付")}}</text>

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
        margin-top: 32px;
        padding-top: 20px;
        padding-bottom: 20px;
        width: 280px;
        color: #ffffff;
        background-color: #00B4FF;
    }
</style>

<script>
    const eeui = app.requireModule('eeui');
    const pay = app.requireModule('eeui/pay');

    require("../i18n");

    export default {
        data() {
            return {
                info: '',
            }
        },
        created() {
            this.addLanguageData("en", {
                "微信/支付宝支付": "wxpay/alipay",
                "微信支付": "wxpay",
                "支付宝支付": "alipay",
                "检测到未安装pay插件，安装详细请登录https://eeui.app/": "No installation of the pay plug-in, please login https://eeui.app/ for installation details",
            });
        },
        methods: {
            viewCode(str) {
                this.openViewCode(str);
            },

            weixinPay() {
                if (typeof pay === 'undefined') {
                    eeui.alert({
                        title: this.lang('温馨提示'),
                        message: this.lang("检测到未安装pay插件，安装详细请登录https://eeui.app/"),
                    });
                    return;
                }
                eeui.loading();
                eeui.ajax({
                    url: 'https://console.eeui.app/api/wxpay',
                    beforeAfter: true,
                }, (result) => {
                    if (result.status === 'complete') {
                        eeui.loadingClose();
                    }
                    if (result.status === 'success') {
                        let data = result.result;
                        if (data.ret === 1) {
                            this.info = "";
                            pay.weixin(data.data, (res) => {
                                this.info = res;
                            });
                        }else{
                            eeui.alert(data.msg);
                        }
                    }
                });
            },

            alipayPay() {
                if (typeof pay === 'undefined') {
                    eeui.alert({
                        title: this.lang('温馨提示'),
                        message: this.lang("检测到未安装pay插件，安装详细请登录https://eeui.app/"),
                    });
                    return;
                }
                eeui.loading();
                eeui.ajax({
                    url: 'https://console.eeui.app/api/alipay',
                    beforeAfter: true,
                }, (result) => {
                    if (result.status === 'complete') {
                        eeui.loadingClose();
                    }
                    if (result.status === 'success') {
                        let data = result.result;
                        if (data.ret === 1) {
                            this.info = "";
                            pay.alipay(data.data.response, (res) => {
                                this.info = res;
                            });
                        }else{
                            eeui.alert(data.msg);
                        }
                    }
                });

            }
        }
    };
</script>
