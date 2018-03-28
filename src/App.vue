<template>
    <div id="app">
        <cnode-head></cnode-head>
        <router-view name='main'></router-view>
        <!--ref用于在 $refs 注册引用信息val-->
    </div>
</template>

<script>
import cnodeHead from './components/cnodeHead';

export default {
    name: 'app',
    data() {
        return {
            authorName: '',
        };
    },
    components: {
        cnodeHead,
    },
    watch: {
        authorName(val) {
            this.$refs.child.name = val;
        },
    },
};
</script>

<style lang="scss">
body,html {
    font-size: 62.5%;
    font-size: 10px/*no*/;
}
#app {
    font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 4rem;
    display: flex;
    justify-content: space-around;
    font-size: 22px/*no*/;
    word-break: break-all;
}

body,
div,
span,
a,
p,
ul,
li {
    margin: 0;
    padding: 0;
}
</style>
