<template>
    <div class='head'>
        <router-link to='/'>
            <img src='../assets/cnodejs.svg' title='cnodejs.svg'>
        </router-link>
        <el-button type='text' @click='dialogVisible=true'>关于</el-button>
        <el-dialog title='Vue.js重写CnodeJS社区' v-model='dialogVisible' size='tiny'>
            <div class='dialogDiv'>
                <span>
                    <strong>作者: &nbsp;&nbsp;</strong>
                </span>
                <a href='http://www.zcbboke.com' target='_blank'>Geekape</a>
                </span>
                <br>
                <span>
                    <strong>源代码: &nbsp;&nbsp;</strong>
                </span>
                <a href='https://github.com/geekape/vue-cnode' target='_blank'>Github</a>
                <span class='star'>&nbsp;&nbsp;求Star</span>
                <br>
                <br>
                <span>
                    <strong>技术栈: </strong>
                </span>
                <ul>
                    <li>Vue.js</li>
                    <li>Vue-router</li>
                    <li>Axios</li>
                    <li>Element</li>
                    <li>CnodeJS API</li>
                </ul>
            </div>
        </el-dialog>
    </div>
</template>

<script>
export default {
    data() {
        return {
            dialogVisible: false,
        };
    },
};
</script>

<style lang="scss">
@import url("https://cdn.bootcss.com/element-ui/1.2.8/theme-default/index.css");
.head {
    background: #324057;
    height: 200px;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    img {
        width: 300px;
        height: 200px;
        margin-left: 30px;
        border:0;
    }
    >button {
        display: inline-block;
        float: right;
        line-height: 3rem;
        margin-right: 30px;
        font-weight: bold;
        font-size: 30px;
        color: white;
        letter-spacing: 2px;

    }
    .dialogDiv {
        font-size: 17px;
    }
    ul {
        margin-left: 20px;
    }
    a {
        text-decoration:none;
        color: #13CE66;
    }
    .star {
        font-weight: bold;
        color: #1D8CE0;
        font-size: 20px;
    }
    .el-dialog {
        width: 60%;
    }
}

</style>
