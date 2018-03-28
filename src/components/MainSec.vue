<template>
    <div class='secDiv' v-loading='loading'>
        <div v-for='item of content' :key='item.id'>
            <router-link :to='{name: "UserRoute",params:{name: item.author.loginname}}'>
                <img :src='item.author.avatar_url' :title='item.author.loginname'>
            </router-link>
            <div class='textDiv'>
                <router-link :to='{name:"ArticleRoute",params:{id:item.id}}'>{{item.title}}</router-link>
                <div class='stuff'>
                    <span>回复：{{item.reply_count}}</span>
                    <span>创建于：{{dealTime(item.create_at)}}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
console.log('Hello,Friend!');

export default {
    name: 'MainSection',
    data() {
        return {
            content: [],
            item: {
                create_at: '2017-02-22T11:32:43.547Z',
            },
            limit: 0,
            loading: true,
        };
    },
    methods: {
        dealTime(time) {
            return time.match(/.{10}/)[0];
        },
        scrollMethod() {
            const sumH = document.body.scrollHeight || document.documentElement.scrollHeight;
            const viewH = document.documentElement.clientHeight;
            const scrollH = document.body.scrollTop || document.documentElement.scrollTop;
            if (viewH + scrollH >= sumH) {
                this.getData();
            }
        },
        getData() {
            this.limit += 10;
            this.$http({
                url: 'https://cnodejs.org/api/v1/topics',
                method: 'get',
                params: {
                    page: 1,
                    limit: this.limit,
                    mdrender: 'false',
                },
            }).then((res) => {
                this.content = res.data.data;
            }).catch((res) => {
                console.log('MaiSec.vue: ', res);
            });

        },
    },
    // 页面渲染完毕后执行
    mounted() {
        window.addEventListener('scroll', this.scrollMethod);
    },
    
    // 实例创建完成后被立即调用
    created() {
        this.getData();
    },

    // 内容加载完成后去除loading
    watch: {
        content(val) {
            if (val) {
                this.loading = false;
            }
        },
    },
};
</script>

<style scoped>
.secDiv {
    width: 90%;
    background: #F9FAFC;
    border: 1px solid #ddd;
    display: flex;
    flex-direction: column;
    font-size: 22px;
    padding: 20px;
    min-height: 30px;
}

a {
    text-decoration: none;
}

.secDiv>div {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    margin: 5px 0;
    border-bottom: 2px solid #C0CCDA;
    padding-bottom: 20px;
}

.secDiv>div img {
    width: 100px;
    height: 100px;
    margin-right: 30px;
}

.textDiv {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    width: 100%;
}

.textDiv a {
    color: black;
    font-size: 25px;
}

.textDiv a:visited {
    color: grey;
}

.stuff {
    font-size: 17px;
    margin-top: 16px;
    color: #8492A6;
}

.stuff span:first-child {
    margin-right: 50px;
}
</style>
