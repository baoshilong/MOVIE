<template>
    <header-bar left="back" right="search" :title="title"></header-bar>
    <div class="top"><film  :m-data="modules"></film></div>
    <loading :show="$loadingRouteData"></loading>
</template>
<script>
    export default{
        data(){
            return {
                title: '电影',
                modules: {},
                words: []

            }
        },

        route: {
            data (transition) {
                document.title = this.title

                const actions = ['in_theaters', 'coming_soon', 'top250']

                var modules = [];
                var hotwords = [];



                var promiseActions = actions.map((item, index) => {
                    return () => {
                    return this.$http.jsonp('https://api.douban.com/v2/movie/' + item, {count: 9}).then((response) => {
                                modules.push({
                                name: item,
                                title: response.data.title.split('-')[0],
                                total: response.data.total,
                                list: response.data.subjects
                            });

                    response.data.subjects.forEach((item) => {
                        hotwords.push({title: item.title, id: item.id});

                })

                })
                }
            })

                promiseActions.reduce((curr, next) => {
                    return curr.then(next);
            }, Promise.resolve()).then(() => {
                    transition.next({modules: modules})
                sessionStorage.hotwords = JSON.stringify(hotwords)

                this.$loadingRouteData = false
            });
            }
        },
        components:{
            headerBar:require("../components/HeaderBar.vue"),
            film:require("../components/film.vue"),
            loading: require('../components/Loading.vue')
        }
    }

</script>
<style lang="sass" scoped>
.top{
    position: relative;
    top:45px;
}
</style>