<template>
    <div id="flexSection" class="swiper-container">
        <div class="swiper-wrapper">
            <section class="ui-panel swiper-slide" v-for="module in mData">
                <div id="nav"v-link="{name:'list', params: {type: module.name}}">
                    <div></div>
                    <h2>
                    {{title[module.title]}}
                    </h2>
                    <i class="ui-icon-arrow"></i>
                </div>
            <ul class="ui-grid-trisect">
                <li v-for="r in module.list" v-link="{name:'show', params:{id: r.id}}">
                    <div class="ui-grid-trisect-img">
                        <img :src="r.images.large" alt="">
                        <p class="ui-nowrap">{{r.title}}</p>
                    </div>
                </li>
            </ul>
            </section>
        </div>

    </div>
    <div class="pagination swiper-pagination swiper-pagination-bullets"></div>

</template>
<script>
    var Swiper=require('../assets/swiper-3.4.2.min.js');
    export default{
        props:['mData'],
        data(){
          return {
              title:{
                  正在上映的电影:'正在热映',
                  即将上映的电影:'马上上映',
                  豆瓣电影Top250:'历史好评'
              }

          }
        },
        /*computed(){
          return{
              activeTitle(){
                  return {
                      'ui-reddot':swiperActive}
              }
          }
        },*/

        ready(){
           var swiper =new Swiper('.swiper-container',{
               pagination : '.swiper-pagination',
               paginationClickable: true,
               longSwipesRatio: 0.3,
               touchRatio:1,
               observer:true,//修改swiper自己或子元素时，自动初始化swiper
               observeParents:true,//修改swiper的父元素时，自动初始化swiper
               watchSlidesProgress : true
           });





        }

    }

</script>
<style lang="sass" scoped>
    @import '../assets/swiper-3.4.2.min.css';
    .ui-panel {
        padding-bottom: 5px;


    .ui-grid-trisect {
    li {
        position: relative;

    p {
        position: absolute;
        bottom: 0px;
        height: 30px;
        line-height: 30px;
        color: #fff;
        width: 100%;
        text-align: center;
        font-size: 14px;
        background: rgba(0,0,0,0.6);
        padding:0px 5px;
    }
    }
    }

    }

        #nav{
            display: flex;
            flex-direction: row;
            justify-content: space-between;
            div{
                width: 44px;
            }
        }

        h2{

            color: #18b4ed;
        }
        .pagination{
            width: 100%;
            *{
                margin:0 5px;;
            }
           /* display: flex;
            justify-content: center;*/
        }



    .s{
          height:20px;
          width:25%;
          background-color: deepskyblue;
      }

</style>