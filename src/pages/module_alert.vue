<template>
    <div class="app">

        <navbar class="navbar">
            <navbar-item type="back"></navbar-item>
            <navbar-item type="title">
                <text class="title">{{lang("确认对话框")}}</text>
            </navbar-item>
            <navbar-item type="right" @click="viewCode('module/alert')">
                <icon content="md-code-working" class="iconr"></icon>
            </navbar-item>
        </navbar>

        <div class="content">
            <text class="button" @click="toAlert">alert</text>
            <text class="button" @click="toAlert2">alert {{lang("带标题")}}</text>
            <text class="button" @click="toConfirm">confirm</text>
            <text class="button" @click="toConfirm2">confirm {{lang("3个按钮")}}</text>
            <text class="button" @click="toInput">input</text>
            <text class="button" @click="toInput2">input {{lang("2个输入框")}}</text>
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
        margin-top: 16px;
        margin-bottom: 16px;
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
                "带标题": "Attach a title",
                "3个按钮": "Three buttons",
                "2个输入框": "2 input boxes",
                "感谢你使用EEUI！": "Thank you for using EEUI!",
                "确定感谢你使用EEUI！": "Thank you again for using EEUI!",
                "点击了确定！": "Click ok!",
                "点击了：": "Click: ",
                "第三个按钮": "Third button",
                "输入昵称和真实姓名": "Enter Nickname and Realname",
                "请输入昵称": "Enter Nickname",
                "请输入真实姓名": "Enter Realname",
                "昵称：": "Nickname: ",
                "，真实姓名：": ", Realname: ",
            });
        },
        methods: {
            viewCode(str) {
                this.openViewCode(str);
            },
            toAlert() {
                eeui.alert(this.lang('感谢你使用EEUI！'), () => {
                    eeui.toast(this.lang("点击了确定！"))
                });

            },
            toAlert2() {
                eeui.alert({
                    title: this.lang('温馨提示'),
                    message: this.lang('感谢你使用EEUI！'),
                }, () => {
                    eeui.toast(this.lang("点击了确定！"))
                });
            },
            toConfirm() {
                eeui.confirm(this.lang("确定感谢你使用EEUI！"), (result) => {
                    if (result.status == "click") {
                        eeui.toast(this.lang("点击了：") + result.title)
                    }
                });
            },
            toConfirm2() {
                eeui.confirm({
                    title: this.lang("温馨提示"),
                    message: this.lang("确定感谢你使用EEUI！"),
                    buttons: [this.lang("取消"), this.lang("确定"), this.lang("第三个按钮")],
                }, (result) => {
                    if (result.status == "click") {
                        eeui.toast(this.lang("点击了：") + result.title)
                    }
                });
            },
            toInput() {
                eeui.input({
                    title: this.lang("请输入昵称"),
                    buttons: [this.lang("取消"), this.lang("确定")],
                    inputs:[{
                        type: 'text',
                    }]
                }, (result) => {
                    if (result.status == "click" && result.title == this.lang("确定")) {
                        eeui.toast(this.lang("昵称：") + result.data[0])
                    }
                });
            },
            toInput2() {
                eeui.input({
                    title: this.lang("输入昵称和真实姓名"),
                    buttons: [this.lang("取消"), this.lang("确定")],
                    inputs:[{
                        type: 'text',
                        placeholder: this.lang('请输入昵称'),
                    },{
                        type: 'text',
                        placeholder: this.lang('请输入真实姓名'),
                    }]
                }, (result) => {
                    if (result.status == "click" && result.title == this.lang("确定")) {
                        eeui.toast(this.lang("昵称：") + result.data[0] + this.lang("，真实姓名：") + result.data[1])
                    }
                });
            }
        }
    };
</script>
