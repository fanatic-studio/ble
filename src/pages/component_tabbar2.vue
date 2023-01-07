<template>
    <div class="app">

        <tabbar
                ref="reflectName"
                class="tabbar"
                :eeui="{ tabType: 'top', textBold:2 }"
                :tabPages="tabPages"></tabbar>

    </div>
</template>

<style>
    .app {
        flex: 1
    }

    .tabbar {
        flex: 1;
        width: 750px;
    }
</style>

<script>
    require("../i18n");

    export default {
        data() {
            return {
                tabPages: [],
            }
        },
        created() {
            this.addLanguageData("en", {
                "首页": "Home",
                "好友": "Friends",
                "圈子": "Club",
                "设置": "Setting",
            });
        },
        mounted() {
            this.tabPages = [
                    {
                        title: this.lang('首页'),
                        url: 'http://dotwe.org/raw/dist/b5fd96d8d790f0100bdfc20b93eedf09.bundle.wx',
                    },
                    {
                        title: this.lang('好友'),
                        url: 'http://dotwe.org/raw/dist/ba938c9aaebe41e5f60b98f90bd0bf61.bundle.wx',
                        message: 9
                    },
                    {
                        title: this.lang('圈子'),
                        url: 'http://dotwe.org/raw/dist/fb6f016b0116969b6b503e1d3a35285f.bundle.wx',
                        message: 18
                    },
                    {
                        title: this.lang('设置'),
                        url: 'http://dotwe.org/raw/dist/ad0045a7cff0b3a680d9de6dd4806e81.bundle.wx',
                        dot: true
                    },
                ];
        },
    };
</script>
