<template>
    <div class="app">

        <tabbar
                ref="reflectName"
                class="tabbar"
                :eeui="{ tabType: 'bottom' }"
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
                        selectedIcon: 'tb-home',
                        url: 'http://dotwe.org/raw/dist/b5fd96d8d790f0100bdfc20b93eedf09.bundle.wx',
                    },
                    {
                        title: this.lang('好友'),
                        selectedIcon: 'https://eeui.app/assets/images/cartoon/m7.png',
                        unSelectedIcon: 'https://eeui.app/assets/images/cartoon/m8.png',
                        url: 'http://dotwe.org/raw/dist/ba938c9aaebe41e5f60b98f90bd0bf61.bundle.wx',
                        message: 9
                    },
                    {
                        title: this.lang('圈子'),
                        selectedIcon: 'md-aperture',
                        url: 'http://dotwe.org/raw/dist/fb6f016b0116969b6b503e1d3a35285f.bundle.wx',
                        message: 18
                    },
                    {
                        title: this.lang('设置'),
                        selectedIcon: 'md-settings',
                        unSelectedIcon: 'md-settings',
                        url: 'http://dotwe.org/raw/dist/ad0045a7cff0b3a680d9de6dd4806e81.bundle.wx',
                        dot: true
                    },
                ];
        },
    };
</script>
