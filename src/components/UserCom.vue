<template>
    <div class='secDiv'>
        <div class='profile' v-loading.lock='loading'>
            <div>
                <img :src='userInfo.avatar_url' :title='userInfo.loginname'>
                <span>{{userInfo.loginname}}</span>
            </div>
            <p>
                <icon name='score' scale='4'></icon>
                <span>积分：</span>{{userInfo.score}}</p>
            <p>
                <icon name='github' scale='4'></icon>
                <span>Github：</span> https://github.com/{{userInfo.githubUsername}}</p>
            <p>
                <icon name='time' scale='4'></icon>
                <span>注册时间：</span>{{dealCommentTime(userInfo.create_at)}}</p>
        </div>

        <div class='recentReplies' v-loading.lock='loading'>
            <p>最近参与的话题</p>
            <template v-for='(item,index) of userInfo.recent_replies'>
                <div v-if='index < 4' :key='index'>
                    <router-link :to='{name: "UserRoute",params:{name: item.author.loginname}}'>
                        <img :src='item.author.avatar_url' :title='item.author.loginname'>
                    </router-link>
                    <router-link :to='{name: "ArticleRoute",params:{id:item.id}}'>
                        <p class='userTitle'>{{item.title}}</p>
                    </router-link>
                </div>
            </template>
        </div>

        <div class='recentTopics' v-loading.lock='loading'>
            <p>最近创建的话题</p>
            <template v-for='(item,index) of userInfo.recent_topics'>
                <div v-if='index < 5 && item' :key='index'>
                    <img :src='item.author.avatar_url' :title='item.author.loginname'>
                    <router-link :to='{name: "ArticleRoute",params:{id:item.id}}'>
                        <p class='userTitle'>{{item.title}}</p>
                    </router-link>
                </div>
            </template>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            userInfo: {
                create_at: '2017-03-20',  //预设默认值：因为Vue会在一系列的初试化过程中调用此数据多次，而此时还有axios还没有执行到。如果没有默认值的话，会因为dealCommentTime中的方法保错：  0 of undefined....
            },
            loading: true,
        };
    },
    created() {
        this.$http({
            url: `https://cnodejs.org/api/v1${this.$route.path}`,
            method: 'get',
        }).then((res) => {
            this.userInfo = res.data.data;
        }).catch((res) => {
            console.log('UserCom.vue: ', res);
        });
    },
    methods: {
        dealCommentTime(time) {
            return String(time).match(/.{10}/)[0].replace(/.{2}/, '').replace(/[T]/, ' ');
        },
    },
    beforeRouteUpdate(to, from, next) {
        this.$http({
            url: `https://cnodejs.org/api/v1${to.path}`,
            method: 'get',
        }).then((res) => {
            this.userInfo = res.data.data;
        }).catch((res) => {
            console.log('UserCom.vue: ', res);
        });
        next();
    },
    
    watch: {
        userInfo(val) {
            if (val) {
                this.loading = false;
            }
        },
    },
};
</script>

<style lang="scss" scoped>
@import url('../assets/css/user.scss');

</style>
