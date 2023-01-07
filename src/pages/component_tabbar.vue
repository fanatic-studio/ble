<template>
    <div class="app">

        <tabbar
                ref="reflectName"
                class="tabbar"
                :eeui="{ tabType: 'bottom' }"
                @pageSelected="pageSelected"
                @tabReselect="tabReselect">

            <!--页签①-->
            <tabbar-page ref="name_1" @refreshListener="refreshListener"
                         :eeui="{ tabName: 'name_1', title:lang('首页'), selectedIcon:'md-home' }">
                <navbar class="page-navbar">
                    <navbar-item type="back"></navbar-item>
                    <navbar-item type="title">
                        <text class="page-navbar-title">{{lang("首页")}}</text>
                    </navbar-item>
                    <navbar-item type="right" @click="viewCode('component/tabbar')">
                        <icon content="md-code-working" class="iconr"></icon>
                    </navbar-item>
                </navbar>
                <div class="page-content">
                    <image src="https://eeui.app/assets/images/cartoon/m2.png" class="page-content-image"></image>
                    <text class="content-text">{{lang("页签里面可以放任何子组件，感谢你对eeui的支持")}}</text>
                </div>
            </tabbar-page>

            <!--页签②-->
            <tabbar-page ref="name_2" @refreshListener="refreshListener"
                         :eeui="{ tabName: 'name_2', title:lang('好友'), message:3, selectedIcon:'https://eeui.app/assets/images/cartoon/m8.png' , unSelectedIcon:'https://eeui.app/assets/images/cartoon/m7.png' }">
                <navbar class="page-navbar">
                    <navbar-item type="title">
                        <text class="page-navbar-title">{{lang("好友")}}</text>
                    </navbar-item>
                </navbar>
                <div class="page-content">
                    <text class="content-text">page 2, {{lang("tab显示器图标支持网络图片")}}</text>
                </div>
            </tabbar-page>

            <!--页签③-->
            <tabbar-page ref="name_3" @refreshListener="refreshListener"
                         :eeui="{ tabName: 'name_3', title:lang('圈子'), message:99, selectedIcon:'md-aperture' }">
                <navbar class="page-navbar">
                    <navbar-item type="title">
                        <text class="page-navbar-title">{{lang("圈子")}}</text>
                    </navbar-item>
                </navbar>
                <div class="page-content">
                    <text v-for="i in 20" class="content-text">{{lang("长页面占位")}} {{i}}</text>
                </div>
            </tabbar-page>

            <!--页签④-->
            <tabbar-page ref="name_4" @refreshListener="refreshListener"
                         :eeui="{ tabName: 'name_4', title:lang('设置'), dot:true, selectedIcon:'md-cog' }">
                <navbar class="page-navbar">
                    <navbar-item type="title">
                        <text class="page-navbar-title">{{lang("设置")}}</text>
                    </navbar-item>
                </navbar>
                <div class="page-content">
                    <text class="content-text">page 4</text>
                </div>
            </tabbar-page>

        </tabbar>

    </div>
</template>

<style>
    .app {
        flex: 1
    }

    .iconr {
        width: 100px;
        height: 100px;
        color: #ffffff;
    }

    .tabbar {
        width: 750px;
        flex: 1;
    }

    .page-content {
        width: 750px;
        padding-top: 200px;
        padding-bottom: 200px;
        align-items: center;
    }

    .content-text {
        font-size: 24px;
        padding: 20px;
    }

    .page-navbar {
        width: 750px;
        height: 90px;
    }

    .page-navbar-title {
        color: #ffffff;
        font-size: 28px;
    }

    .page-content-image {
        width: 480px;
        height: 480px;
        margin-top: 30px;
        margin-bottom: 30px;
    }
</style>

<script>
    const eeui = app.requireModule('eeui');

    require("../i18n");

    export default {
        created() {
            this.addLanguageData("en", {
                "首页": "Home",
                "好友": "Friends",
                "圈子": "Club",
                "设置": "Setting",
                "页签里面可以放任何子组件，感谢你对eeui的支持": "You can put any child components in the TAB. Thank you for supporting eeui",
                "tab显示器图标支持网络图片": "TAB display ICONS support web images",
                "长页面占位": "Long page space",
                "切换到第": "Switch to ",
                "个标签页": " TAB",
                "第": "The ",
                "个标签页被再次点击": " TAB is clicked again",
                "刷新成功": "Refresh the success",
            });
        },
        methods: {
            viewCode(str) {
                this.openViewCode(str);
            },
            pageSelected(params) {
                eeui.toast({
                    message: this.lang("切换到第") + (params.position + 1) + this.lang("个标签页"),
                    gravity: "middle"
                });
            },
            tabReselect(params) {
                eeui.toast({
                    message: this.lang("第") + (params.position + 1) + this.lang("个标签页被再次点击"),
                    gravity: "middle"
                });
                eeui.toast();
            },
            refreshListener(params) {
                setTimeout(() => {
                    eeui.toast({
                        message: this.lang("刷新成功") + ": " + params.tabName,
                        gravity: "middle"
                    });
                    this.$refs[params.tabName].refreshEnd();
                }, 1000);
            }
        }
    };
</script>
