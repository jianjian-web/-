<template>
  <div class="home">
    <div class='TopRightBg'>
      <img src="../assets/img/bg_big_nor.png" alt="">
    </div>
    <div class='wrapper'>
      <my-header></my-header>
      <div class='headText'>
        <p class='title'>我们为您提供更贴近客户的回访解决方案</p>
        <p class='content'>
          智能化客户回访及数据分析，让您节约成本的同时，获得可观 <br> 的反馈回报，时间投入得到更充分的应用。
        </p>
      </div>
      <p class='partTitle'><span>产品的功能</span></p>
      <ul class="product">
        <li v-for='(item,index) in productData' :key='index' @mouseenter="handleOver(index)" @mouseleave='handleOver(index)'>
          <img :src="item.url">
          <p v-text='item.title' class='productTitle'></p>
          <p v-text='item.content' class='txt'></p>
        </li>
      </ul>
       <p class='partTitle' style='margin-top:65px;'><span>工作过程可监控</span></p>
       <p class='part2'>
         沟通过程全程录音，任务完成提交录音文件，方便<br>追踪挖掘客户的深层需求并确保<br>企业信息的安全
       </p>
    </div>
  <div class='voice'>
    <audio controls ref='audio' style='position: absolute;'>
      <source src="../assets/audio/test.mp3" type="audio/mp3" >
    </audio>
    <div class='wrapper'>
      <p class='voiceTitle'>录音过程示范</p>
      <img src="../assets/img/icon_voice_nor.png" alt="">
      <div class='voiceProgress'>
        <i>(部分音源片段因为隐私已屏蔽处理)</i>
           <div class='voiceLeft' :style="{ width: progress+'%' }">
            <div class='voicePoint' @click='play=!play'>
              <span class='point1'></span>
              <span class='point2'></span>
            </div>  
           </div>   <!--// 已经播放的进度 -->
      </div>
      <span class='startTime'>{{currentTime}}</span>
      <span class='endTime'>{{duration}}</span>
    </div>
  </div>
  <div class='wrapper footWrapper'>
    <div class='foot'>
      <div class='item' v-for='(item,index) in footData' :key='index'>
        <img :src="item.img">
        <div class='itemRight'>
          <p class='itemTitle' v-text='item.title'></p>
          <p class='itemContent' v-text='item.content'></p>
        </div>
      </div>
    </div>
    <div class='LeftBottomBg'><img src="../assets/img/bg_small_nor.png"></div>
  </div>
  </div>
</template>
 
<script>
import myHeader from './Header'
export default {
  name: 'home',
  data () {
    return {
      currentTime: 0,
      duration: 0,
      progress: 0,
      play: false,
      audioDom: null,
      productData: [
        {
          url: require('../assets/img/icon_1.png'),
          hoverUrl: require('../assets/img/icon_1_hover.png'),
          title: '高品质的回访',
          content: '智能筛选的回访客户系统，为您匹配最佳的回访者选择方案回访过程全程录音，保障您的信息安全，贴合公司气质，提升企业形象'
        },
        {
          url: require('../assets/img/icon_2.png'),
          hoverUrl: require('../assets/img/icon_2_hover.png'),
          title: '高效的回访节奏',
          content: '智能化系统根据您设置的回访时间间隔，自动发布需求，信息反馈数据集成自动化'
        },
        {
          url: require('../assets/img/icon_3.png'),
          hoverUrl: require('../assets/img/icon_3_hover.png'),
          title: '投入的高性价比',
          content: '提高客户回访的信息转化率及经济回报率'
        },
        {
          url: require('../assets/img/icon_4.png'),
          hoverUrl: require('../assets/img/icon_4_hover.png'),
          title: '增加您的投资回报',
          content: '可设置回访的时间频率，根据行业，目的，有效分类，增强客户粘度'
        },
        {
          url: require('../assets/img/icon_5.png'),
          hoverUrl: require('../assets/img/icon_5_hover.png'),
          title: 'crm集成',
          content: '与您的crm系统同步，智能化导入客户通讯录，创建客户画像，提高回访有效率'
        },
        {
          url: require('../assets/img/icon_6.png'),
          hoverUrl: require('../assets/img/icon_6_hover.png'),
          title: '降低您的成本',
          content: '实时发布回访需求，为您节省组建客服团队的时间及资金投入成本'
        }
      ],
      footData: [
        {
          img: require('../assets/img/icon_question_nor.png'),
          title: '创建客户问卷',
          content: '创建您自己的问题或从您的行业中的其他人正在使用或创建的问卷列表中进行选择，创建个性化，定制化，针对性强的问卷，提高行业回报率'
        },
        {
          img: require('../assets/img/icon_recognize_nor.png'),
          title: '跟踪并衡量客户满意度',
          content: '通过系统智能化检测多个调查期的数据对比，追踪客户满意度，进而回应有效的解决办法，提升顾客满意度'
        },
        {
          img: require('../assets/img/icon_follow_nor.png'),
          title: '识别风险客户',
          content: '根据一段时间调查数据的分析，识别出有风险的客户，并通过系统及时通知您，以方便您快速解决客户的问题'
        }
      ]
    }
  },
  components: {
    myHeader
  },
  methods: {
    handleOver (e) {
      let str = this.productData[e].url
      this.productData[e].url = this.productData[e].hoverUrl
      this.productData[e].hoverUrl = str
    },
    startAudio () {
      this.audioDom.play()
    },
    pauseAudio () {
      this.audioDom.pause()
    },
    getTime () {
      this.timer = setInterval(() => {
        const time = parseInt(this.audioDom.currentTime)
        console.log(Math.floor(time / 60) + ':' + (time % 60 / 100).toFixed(2).slice(-2))
        this.progress = (this.currentTime / this.duration) * 100
      }, 1000)
    }
  },
  mounted () {
    this.audioDom = this.$refs.audio
    this.audioDom.addEventListener('canplay', () => {
      this.duration = parseInt(this.audioDom.duration)
    })
  },
  watch: {
    play (v) {
      if (v) {
        this.startAudio()
        this.getTime()
      } else {
        this.pauseAudio()
        clearInterval(this.timer)
        this.timer = null
      }
    }
  }
}
</script>

<style scoped lang=less>
@import url('../assets/css/base.less');
  .home{
    overflow: hidden;
    position: relative;
    padding-top:40px;
    .TopRightBg{
      position: absolute;
      z-index:-1;
      top:0;
      right: 0;
      width:60%;
      height:800px;
      img{
        width:100%;
        height:auto;
      }
    } 
    .headText{
      padding-left:20px;
      margin-top:200px;
      margin-bottom:250px;
      .title{
        font-size:34px;
        margin-bottom:45px;
      }
      .content{
        font-size:24px;
        color:#666;
        line-height: 36px;
      }
    }
    .partTitle{
      font-size:24px;
      text-align: center;
      span{
        border-bottom:1px solid #000;      
        padding-bottom:5px;  
      }
    }
    .product{ 
      display: flex;
      margin-top:15px;
      padding:0 80px;  
      flex-direction: row;
      flex-wrap: wrap;
      justify-content: space-between;
      li{
        border-radius: 12px;
        margin:80px 20px;
        width:250px;
        height:370px;
        border:1px solid #d2d2d2;
        transition: all 0.35s ease-out; 
        text-align: center;
        background:#f9f9f9;
        &:hover{
          box-shadow: 0 0 30px #ccc;
          transform: scale(1.152);
          font-size:1.2em;
          border:0;
          background:#fff;
          img{
            box-shadow: 0 10px 20px #ccc;
            border-radius: 50%;
          }
        }
        img{
          margin-top:2.4em;
          margin-bottom:2.2em;
        }
        .productTitle{
          font-size:1.143em ;
        }
        .txt{
          width:13.57em;
          margin: 0 auto;
          margin-top:1.5em;
          color:#757474;
          line-height: 1.5em;
          padding-bottom:1em;
        }
      }
    }
    .part2{
      /* width:308px; */
      line-height: 24px;
      margin:0 auto;
      text-align: center;
      color:#4d4d4d;
      margin-top:40px;
    }
    .voice{
      height: 240px;
      background: #eeeeee;
      margin-top:67px;
      line-height: 240px;
      margin-bottom:120px;
      img{
        vertical-align: middle;
        box-shadow: 0 0 50px #666;
        border-radius: 63px;
        -webkit-animation-name: breathingLight;
        -webkit-animation-duration: 2s;
        -webkit-animation-iteration-count: infinite;
      }
      @keyframes breathingLight {
        from {
          box-shadow: 0 0 50px #666;
        }
        50% {
          box-shadow: 0 0 10px @baseColor;
        }
        to {
          -webkit-box-shadow:0 0 50px #666;
        }
      }
      .wrapper{
      padding-left:75px;        
        position: relative;
        .voiceTitle{
          position: absolute;
          line-height: 18px;
          font-size: 18px;
          top:30px;
          left: 0;
          width:100%;
          text-align: center;
        }
        .voiceProgress{
          display: inline-block;
          height: 8px;
          width:716px;
          background:#a0a0a0;
          margin-left:130px;
          position: relative;
          i{
            line-height: 12px;
            font-size: 12px;
            position: absolute;
            left: 50%;
            top:20px;
            font-style: normal;
            transform: translate(-50%,0);
          }
          .voiceLeft{
            background:#008DF8;
            height:8px;
            width:0%;
            position: relative;
            .voicePoint{
              z-index:5;
              cursor: pointer;
              width:54px;
              height: 54px;
              background:rgba(54,151,250,0.5);
              border-radius: 27px;
              position: absolute;
              top:-23px;
              right:-20px;
              .point1{
                position: absolute;
                width:36px;
                height: 36px;
                background: #eee;
                opacity: 0.8;
                left: 50%;
                top:50%;
                transform: translate(-50%,-50%);
                border-radius: 18px;
              }
              .point2{
                position: absolute;
                width:16px;
                height: 16px;
                background: #7d7d7d;
                opacity: 0.8;
                left: 50%;
                top:50%;
                transform: translate(-50%,-50%);
                border-radius: 8px;
              }
            }
          }
        }
        .startTime{
          position: absolute;
          left:335px;
          top:40px;
        }
        .endTime{
          position: absolute;
          left:1026px;
          top:40px;
        }
      }
    }
    .footWrapper{
      /* overflow: hidden; */
      .foot{
        padding-left:219px;
        margin-bottom: 320px;
        .item{
          display: flex;
          flex-direction: row;
          margin-bottom:75px;
          img{
            margin-right:100px;
          }
          .itemRight{
            .itemTitle{
              font-size:18px;
              color:#255ce4;
              margin-top:10px;
              margin-bottom:30px;
              border-left:6px solid #255ce4;
              padding-left:15px;
            }
            .itemContent{
              width:624px;
              font-size: 16px;
              line-height: 25px;
              padding-left:20px;
            }
          }
        }
      }
      .LeftBottomBg{
        position: absolute;
        left:0;
        bottom:-5px; 
        width:45%;
        z-index:-1;
        img{
          width:80%;
          height:auto;
        }
      }
    }
  }
</style>
