<template>
    <div class='container'>
        <!-- 休闲娱乐 -->
        <div class='main'>
            <ul v-if='isShow'>
                <li>
                    <img src="~/assets/images/4.jpg" alt="">
                    <p class='storeName'>仙剑奇侠传</p>
                    <span class='moods'>人气98</span>
                    <img src="~assets/images/flame.png" alt="" class='flame'><img src="~assets/images/flame.png" alt="" class='flame'><img src="~assets/images/flame.png" alt="" class='flame'>
                    <span class='averagePrice'>人均120元</span>
                    <span class='distance'>10000km</span>
                    <div class='welfale'>周一至周五/男生半价</div>
                    <span class='price'>200yuan</span>
                    <span class='lyPrice'>300yuan</span>
                </li>
            </ul>
        </div>
        <div class='noStore' v-if='!isShow'>
            <img src="~/assets/images/noStore.png" alt="">
            <p>暂无商家入驻，敬请期待...</p>
        </div>
    </div>
</template>
<script>
import api from "~/api";
import ts from "coordtransform";

export default {
    head() {
        return {
            title: "休闲娱乐"
        };
    },
    data() {
        return {
            isShow: false,
            params: {
                typeid: 3,
                pageNum: 1,
                pageSize: 3,
                lng: this.$store.state.coordinate.lng,
                lat: this.$store.state.coordinate.lat,
            }
        };
    },
    mounted() {
        console.log(this.params,11)
        /* 娱乐相关的商家 */
        api.getPlayStore(this.params).then(res => {
            if(res.data==null) {
                this.isShow=false;
            } else {
            }
            console.log(res,55)
        });
    }
};
</script>

<style lang='scss' scoped>
@import "~@/assets/style/px-to-rem";
.container {
  width: 100%;
  height: 100%;
  background-color: #fff;
}
.main {
  width: 100%;
  background-color: #fff;
  overflow: hidden;
  ul {
    width: 100%;
    li {
      position: relative;
      width: 100%;
      padding: tr(30px);
      box-sizing: border-box;
      border-bottom: 1px solid #eee;
      overflow: hidden;
      > img:nth-child(1) {
        background-color: pink;
        width: tr(210px);
        height: tr(190px);
        border-radius: tr(5px);
        float: left;
        margin-right: tr(20px);
      }
      .storeName {
        margin-top: tr(6px);
        font-size: tr(30px);
        color: #000;
      }
      .moods {
        margin-top: tr(10px);
        display: inline-block;
        color: #ff1400;
        font-size: tr(28px);
        margin-right: tr(12px);
        vertical-align: middle;
      }
      .flame {
        margin-top: tr(10px);
        width: tr(30px);
      }
      .averagePrice {
        margin-top: tr(10px);
        display: inline-block;
        margin-left: tr(20px);
        vertical-align: middle;
        color: #999;
      }
      .distance {
        float: right;
        margin-top: tr(15px);
        color: #999;
      }
      .welfale {
        margin-top: tr(20px);
        position: absolute;
        left: tr(260px);
        font-size: tr(24px);
        color: #999;
      }
      .price {
        position: absolute;
        bottom: tr(20px);
        left: tr(260px);
        display: inline-block;
        color: #ff1400;
        font-size: tr(26px);
      }
      .lyPrice {
        position: absolute;
        bottom: tr(20px);
        left: tr(380px);
        text-decoration: line-through;
        color: #999;
        font-size: tr(26px);
      }
    }
  }
}
.noStore {
  width: 100%;
  position: absolute;
  left: 50%;
  top: 30%;
  transform: translateX(-50%);
  img {
    width: tr(210px);
    height: tr(168px);
    position: relative;
    left: 50%;
    transform: translateX(-50%);
  }
  p {
    color: RGBA(153, 153, 153, 1);
    font-size: tr(24px);
    text-align: center;
    margin-top: tr(20px);
  }
}
</style>
