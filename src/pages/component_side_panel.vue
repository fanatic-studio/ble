<template>
    <div class="app">

        <side-panel
                ref="reflectName"
                class="side_panel"
                :eeui="{
                        width: '420px',
                        scrollbar: false,
                        backgroundColor: '#26c9ff'
                    }"
                @itemClick="itemClick"
                @switchListener="switchListener">

            <!--侧滑菜单部分-->
            <side-panel-menu class="panel_menu" :name="lang('菜单1')">
                <text class="menu-text">{{lang("菜单①")}}</text>
            </side-panel-menu>

            <side-panel-menu class="panel_menu" :name="lang('菜单2')">
                <text class="menu-text">{{lang("菜单②")}}</text>
            </side-panel-menu>

            <!--正文内容部分-->
            <div class="content">
                <!--正文标题栏-->
                <navbar class="content-navbar">
                    <navbar-item type="back"></navbar-item>
                    <navbar-item type="title">
                        <text class="title">{{lang("侧边栏")}}</text>
                    </navbar-item>
                    <navbar-item type="right" @click="viewCode('component/side-panel')">
                        <icon content="md-code-working" class="iconr"></icon>
                    </navbar-item>
                </navbar>
                <!--正文内容-->
                <div class="content-body">
                    <text style="font-size:24px">{{lang("正文内容，点击下面的按钮试试。")}}</text>
                    <text class="content-body-toggle" @click="menuToggle">{{lang("切换显示状态")}}</text>
                </div>
            </div>

        </side-panel>

    </div>
</template>

<style scoped>
    .app {
        width: 750px;
        flex: 1;
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

    .side_panel {
        width: 750px;
        flex: 1;
    }

    .panel_menu {
        width: 420px;
        padding-top: 26px;
        padding-bottom: 26px;
        padding-right: 20px;
        padding-left: 20px;
        border-bottom-width: 1px;
        border-bottom-style: solid;
        border-bottom-color: #ffffff;
    }

    .menu-text {
        color: #ffffff;
        font-size: 26px;
    }

    .content {
        width: 750px;
    }

    .content-navbar {
        width: 750px;
        height: 100px;
    }

    .content-body {
        width: 750px;
        margin-top: 200px;
        justify-content: center;
        align-items: center;
    }

    .content-body-toggle {
        width: 300px;
        font-size: 24px;
        text-align: center;
        margin-top: 20px;
        padding-top: 20px;
        padding-bottom: 20px;
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
                "菜单1": "menu1",
                "菜单2": "menu2",
                "菜单①": "menu_1",
                "菜单②": "menu_2",
                "正文内容，点击下面的按钮试试。": "Text content, click the button below.",
                "切换显示状态": "Toggle display state",
                "点击了": "Click ",
                "项，": ", ",
                "显示了": "show",
                "隐藏了": "hide",
            });
        },
        methods: {
            viewCode(str) {
                this.openViewCode(str);
            },
            itemClick(params) {
                eeui.toast(this.lang("点击了") + (params.position + 1) + this.lang("项，") + "name：" + params.name);
            },
            switchListener(params) {
                eeui.toast(this.lang("侧边栏") + ": " + (params.show ? this.lang("显示了") : this.lang("隐藏了")));
            },
            menuToggle() {
                this.$refs.reflectName.menuToggle();
            },
        }
    };
</script>
