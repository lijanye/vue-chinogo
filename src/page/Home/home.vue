<template>
  <div>
    <div class="banner">
      <div ref="bg" :style="bg"
           @mouseover="bgOver($refs.bg)"
           @mousemove="bgMove($refs.bg,$event)"
           @mouseout="bgOut($refs.bg)">
        <span class="a" :style="img"></span>
        <span class="text b" v-html="chinogoText"></span>
        <span class="copyright c" v-html="copyright"></span>
      </div>
    </div>
  </div>
</template>
<script>
  import YShelf from '/components/shelf'
  import product from '/components/product'
  import mallGoods from '/components/mallGoods'
  import { indexHome } from '/api/index'

  export default {
    data () {
      return {
        banner: {},
        bgOpt: {
          px: 0,
          py: 0,
          w: 0,
          h: 0
        },
        floors: [],
        hot: [],
        copyright: 'code by chinotan | picture from chinogo',
        chinogoText: 'chinogo<br/>赛高'
      }
    },
    computed: {
      img () {
        return {
          display: 'block',
          position: 'absolute',
          width: '100%',
          height: '100%',
          bottom: '5px',
          left: '0',
          background: 'url("/static/images/niniji.png") center no-repeat',
          backgroundSize: '95% 100%'
        }
      },
      bg () {
        return {
          position: 'relative',
          width: '1220px',
          height: '500px',
          margin: '20px auto',
          background: 'url("/static/images/miku.jpg") center no-repeat',
          backgroundSize: '100% 100%',
          borderRadius: '10px',
          transformStyle: 'preserve-3d',
          WebkitTransformOrigin: '50% 50%',
          WebkitTransform: 'rotateY(0deg) rotateX(0deg)'
        }
      }
    },
    methods: {
      bgOver (e) {
        this.bgOpt.px = e.offsetLeft
        this.bgOpt.py = e.offsetTop
        this.bgOpt.w = e.offsetWidth
        this.bgOpt.h = e.offsetHeight
      },
      bgMove (dom, eve) {
        let bgOpt = this.bgOpt
        let X, Y
        let mouseX = eve.pageX - bgOpt.px
        let mouseY = eve.pageY - bgOpt.py
        if (mouseX > bgOpt.w / 2) {
          X = mouseX - (bgOpt.w / 2)
        } else {
          X = mouseX - (bgOpt.w / 2)
        }
        if (mouseY > bgOpt.h / 2) {
          Y = bgOpt.h / 2 - mouseY
        } else {
          Y = bgOpt.h / 2 - mouseY
        }
        dom.style['-webkit-transform'] = `rotateY(${X / 50}deg) rotateX(${Y / 50}deg)`
        dom.style.transform = `rotateY(${X / 50}deg) rotateX(${Y / 50}deg)`
      },
      bgOut (dom) {
        dom.style['-webkit-transform'] = 'rotateY(0deg) rotateX(0deg)'
        dom.style.transform = 'rotateY(0deg) rotateX(0deg)'
      }
    },
    created () {
      indexHome(90).then(res => {
        this.img.background = 'url("' + res[0].pic + '") center no-repeat'
      })
      indexHome(89).then(res => {
        this.bg.background = 'url("' + res[0].pic + '") center no-repeat'
      })
      indexHome(98).then(res => {
        this.copyright = res[0].content
      })
      indexHome(91).then(res => {
        this.chinogoText = res[0].content
      })
    },
    components: {
      YShelf,
      product,
      mallGoods
    }
  }
</script>
<style lang="scss" rel="stylesheet/scss" scoped type="text/scss">
  .banner, .banner span, .banner div {
    font-family: "Microsoft YaHei";
    transition: all .3s;
    -webkit-transition: all .3s;
    transition-timing-function: linear;
    -webkit-transition-timing-function: linear;
  }

  .banner {
    perspective: 3000px;
    position: relative;
    z-index: 19;
  }

  .text {
    position: absolute;
    top: 20%;
    right: 10%;
    font-size: 30px;
    color: #fff;
    text-align: right;
    font-weight: lighter;
  }

  .copyright {
    position: absolute;
    bottom: 10%;
    right: 10%;
    font-size: 10px;
    color: #fff;
    text-align: right;
    font-weight: lighter;
  }

  .a {
    -webkit-transform: translateZ(40px);
  }

  .b {
    -webkit-transform: translateZ(20px);
  }

  .c {
    -webkit-transform: translateZ(0px);
  }

  .sk_item {
    width: 170px;
    height: 225px;
    padding: 0 14px 0 15px;
    > div {
      width: 100%;
    }
    a {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      transition: all .3s;
      &:hover {
        transform: translateY(-5px);
      }
    }
    img {
      width: 130px;
      height: 130px;
      margin: 17px 0;
    }
    .sk_item_name {
      color: #999;
      display: block;
      max-width: 100%;
      _width: 100%;
      overflow: hidden;
      font-size: 12px;
      text-align: left;
      height: 32px;
      line-height: 16px;
      word-wrap: break-word;
      word-break: break-all;
    }
    .sk_item_price {
      padding: 3px 0;
      height: 25px;
    }
    .price_new {
      font-size: 18px;
      font-weight: 700;
      margin-right: 8px;
      color: #f10214;
    }
    .price_origin {
      color: #999;
      font-size: 12px;
    }
  }

  .box {
    overflow: hidden;
    position: relative;
    z-index: 0;
    margin-top: 29px;
    box-sizing: border-box;
    border: 1px solid rgba(0, 0, 0, .14);
    border-radius: 8px;
    background: #fff;
    box-shadow: 0 3px 8px -6px rgba(0, 0, 0, .1);

  }

  ul.box {
    display: flex;
    li {
      flex: 1;
      img {
        display: block;
        width: 305px;
        height: 200px;
      }
    }
  }

  .mt30 {
    margin-top: 30px;
  }

  .hot {
    display: flex;
    > div {
      flex: 1;
      width: 25%;
    }
  }

  .floors {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    .imgbanner {
      width: 50%;
      height: 430px;
    }
    img {
      display: block;
      width: 100%;
      height: 100%;
    }
  }

</style>
