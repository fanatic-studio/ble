<template>
    <div class="app">

        <navbar class="navbar">
            <navbar-item type="back"></navbar-item>
            <navbar-item type="title">
                <text class="title">{{title}}</text>
            </navbar-item>
        </navbar>

        <div class="main">
            <WEcharts class="echarts" :options="options"></WEcharts>
            <WEcharts class="echarts" :options="optionpie"></WEcharts>
        </div>
    </div>
</template>

<style scoped>
    .app {
        width: 750px;
        flex: 1;
        background-color: #ffffff;
    }

    .navbar {
        width: 750px;
        height: 100px;
    }

    .title {
        font-size: 28px;
        color: #ffffff
    }

    .main {
        flex: 1;
        justify-content: center;
    }

    .echarts {
        width: 750px;
        height: 750px;
    }
</style>

<script>
    import WEcharts from "../components/WEcharts/index";
    const eeui = app.requireModule('eeui');

    require("../i18n");

    export default {
        components: {WEcharts},
        data() {
            return {
                title: 'Basic Line Chart',
                options: {
                    xAxis: {
                        type: 'category',
                        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
                    },
                    yAxis: {
                        type: 'value'
                    },
                    series: [{
                        data: [820, 932, 901, 934, 1290, 1330, 1320],
                        type: 'line'
                    }]
                },
                // 饼图
                optionpie: {
                    backgroundColor: '#2c343c',

                    title: {
                        text: 'Customized Pie',
                        left: 'center',
                        top: 20,
                        textStyle: {
                            color: '#ccc'
                        }
                    },

                    tooltip: {
                        trigger: 'item',
                        formatter: "{a} <br/>{b} : {c} ({d}%)"
                    },

                    visualMap: {
                        show: false,
                        min: 80,
                        max: 600,
                        inRange: {
                            colorLightness: [0, 1]
                        }
                    },
                    series: [{
                        name: '访问来源',
                        type: 'pie',
                        radius: '55%',
                        center: ['50%', '50%'],
                        data: [
                            { value: 335, name: '直接访问' },
                            { value: 310, name: '邮件营销' },
                            { value: 274, name: '联盟广告' },
                            { value: 235, name: '视频广告' },
                            { value: 400, name: '搜索引擎' }
                        ].sort(function(a, b) { return a.value - b.value; }),
                        roseType: 'radius',
                        label: {
                            normal: {
                                textStyle: {
                                    color: 'rgba(255, 255, 255, 0.3)'
                                }
                            }
                        },
                        labelLine: {
                            normal: {
                                lineStyle: {
                                    color: 'rgba(255, 255, 255, 0.3)'
                                },
                                smooth: 0.2,
                                length: 10,
                                length2: 20
                            }
                        },
                        itemStyle: {
                            normal: {
                                color: '#c23531',
                                shadowBlur: 200,
                                shadowColor: 'rgba(0, 0, 0, 0.5)'
                            }
                        },

                        animationType: 'scale',
                        animationEasing: 'elasticOut',
                        animationDelay: function(idx) {
                            return Math.random() * 200;
                        }
                    }]
                },
            }
        },

        mounted() {
            this.title = app.config.params.title ? app.config.params.title : this.title;
            this.options = app.config.params.options ? JSON.parse(app.config.params.options) : this.options;
        },

        methods: {

        }
    };
</script>
