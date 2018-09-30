<template>
  <div class="bar">
    <!--<button @click="changeEcharts">切换</button>-->
    <div class="bar-top">
      <div class="back-icon"></div>
      <div class="top-title">{{ title }}</div>
    </div>
    <div class="bar-box">
      <div class="border"></div>
      <div class="box-title">
        <p>{{ date }}</p>
        <div class="calendar-icon"></div>
      </div>
      <div class="box-content">
        <div>
          <div class="title">
            <p>
              {{ item1.title }}
              <span class="type" @click="changeType">
                <div :class="selected ? 'white-line' : 'blue-line'"></div>
                <div :class="!selected ? 'white-pie' : 'blue-pie'"></div>
                <div class="tp" :class="showAnim"></div>
              </span>
            </p>
            <div>{{ item1.totalAmt }}</div>
          </div>
          <card :options = 'wxOptions'></card>
          <p class="worth">单笔最贵</p>
          <div class="rank-list">
            <div v-for="item in rankList" class="rank">
              <p><img :src="item.src"/>{{ item.name }}</p>
              <p>{{ item.value }}</p>
            </div>
          </div>
        </div>
        <div>
          <div class="title">
            <p>{{ item2.title }}</p>
            <div>{{ item2.totalAmt }}</div>
          </div>
          <card :options = 'wxOptions2'></card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import card from '../../components/card'

  const data = [
    [1290, 1330, 1320, 820, 932, 901, 934],
    [934, 934, 934, 934, 934, 932, 901]
  ]
  let i = 0

  export default {
    components: {
      card
    },
    data () {
      return {
        title : '月账单',
        date: '2018年9月',
        rankList: [
          {name: '房租水电', value: '1200.00', src: '/dist/assert/img/first.png'},
          {name: '火车票', value: '223.00', src: '/dist/assert/img/second.png'},
          {name: '花味（雨花客厅店）', value: '165.89', src: '/dist/assert/img/third.png'},
        ],
        item1: {
          title: '消费',
          totalAmt: '-2,450.24'
        },
        item2: {
          title: '小买卖',
          totalAmt: '-1,702.6'
        },
        selected: true,
        showAnim: '',
        wxOptions: this.getOptions(0),
        wxOptions2: this.getOptions2(0)
      }
    },
    mounted () {
    },
    methods: {
      changeEcharts: function () {
        if (i) {
          i = 0
        } else {
          i = 1
        }
        setTimeout(() => {
          this.wxOptions = this.getOptions(i)
        }, 3000)
      },
      getOptions: function (i) {
        let option
        if (i===0) {
          option = {
            tooltip: {
              trigger: 'item',
              formatter: "{b}\n {c} ({d}%)"
            },
            series: [
              {
                name:'',
                type:'pie',
                radius: ['30%', '50%'],
                avoidLabelOverlap: false,
                label: {
                  normal: {
                    show: true,
                    position: 'outside',
                    formatter: "{b} \n {c} ({d}%)"
                  },
                  emphasis: {
                    show: true,
                    textStyle: {
                      fontSize: '16',
                      fontWeight: 'bold'
                    }
                  }
                },
                labelLine: {
                  normal: {
                    show: true
                  }
                },
                data:[
                  {name: '通讯物流', value: 29.85},
                  {name: '交通出行', value: 729.83},
                  {name: '健康', value: 26},
                  {name: '饮食', value: 165.89},
                  {name: '生活日用', value: 1281.70},
                  {name: '其他消费', value: 216.88}
                ]
              }
            ]
          }
        } else if (i === 1) {
          option = {
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
          }
        }
        return option
      },
      getOptions2: function (i) {
        let option = {
          color: ['#3398DB'],
          tooltip : {
            trigger: 'axis',
            axisPointer : {
              type : 'line'        // 默认为直线，可选为：'line' | 'shadow'
            }
          },
          grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
          },
          xAxis : [
            {
              type : 'category',
              data : ['收钱码', '淘宝', '闲鱼', '其他'],
              axisTick: {
                alignWithLabel: true
              }
            }
          ],
          yAxis : [
            {
              type : 'value'
            }
          ],
          series : [
            {
              type:'bar',
              barWidth: '40%',
              data:[1024.1, 105.6, 237, 335.9]
            }
          ]
        }
        return option
      },
      changeType () {
        if (this.selected) {
          this.showAnim = 'to-right'

        } else {
          this.showAnim = 'to-left'
        }
        this.selected = !this.selected
      }
    }
  }
</script>

<style>
  .bar {
    height: 100%;
    width: 100%;
    overflow: auto;
    background: #2196F3;
  }
  .bar-top {
    position: fixed;
    height: 50px;
    line-height: 50px;
    display: flex;
    align-items: center;
    color: #ffffff;
    background: #2196F3;
    width: 100%;
    z-index: 2;
  }
  .back-icon {
    height: 20px;
    width: 28px;
    margin-left: 10px;
    background: url("../../../dist/assert/img/back.png") no-repeat;
    background-size: contain;
  }
  .top-title {
    font-size: 16px;
  }
  .bar-box {
    background-color: #ffffff;
    /*background: url("../../../dist/assert/img/grid.png") repeat;*/
    margin: 50px 8px 10px;
    padding: 8px;
    border-radius: 2px;
    position: relative;
    overflow: hidden;
  }
  .border {
    height: 0;
    width: 100%;
    /*background: #000;*/
    border-top: 8px dotted #2196F3;
    margin: 0 8px;
    position: absolute;
    top: -6px;
    left: 0;
  }
  .box-title {
    font-size: 14px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #343434;
    padding: 14px 2px 10px;
    border-bottom: 4px solid;
  }
  .calendar-icon {
    height: 16px;
    width: 16px;
    background: url("../../../dist/assert/img/calendar.png") no-repeat;
    background-size: contain;
  }
  .box-content {
    margin-top: 3px;
    border-top: 1px solid;
  }
  .title {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 20px 2px 10px;
    color: #343434;
  }
  .title p {
    font-size: 18px;
    font-weight: bold;
    height: 20px;
    line-height: 20px;
    border-left: 5px solid;
    padding: 0 10px;
    font-family: monospace;
    display: inline-flex;
    align-items: center;
  }
  .type {
    margin-left: 10px;
    width: 50px;
    height: 25px;
    border-radius: 20px;
    border: 1px solid #a9d0e4;
    position: relative;
  }
  .tp {
    height: 23px;
    width: 23px;
    border-radius: 20px;
    background: #1296db;
    position: absolute;
    top: 1px;
    left: 1px;
  }
  @keyframes anim-right {
    0% { left: 1px; }
    10%{ left: 10% }
    30%{ left: 40% }
    95%{ left: 52% }
    100% { left: 50%;}
  }
  @keyframes anim-left {
    0% { left: 50%; }
    10%{ left: 40% }
    30%{ left: 10% }
    95%{ left: -2% }
    100% { left: 1px; }
  }
  .tp.to-right {
    /*执行动画*/
    -webkit-animation: anim-right 0.5s 1;
    animation: anim-right 0.5s 1;
    /*停止在最后一帧*/
    -webkit-animation-fill-mode:forwards;
    animation-fill-mode:forwards;
  }
  .tp.to-left {
    /*执行动画*/
    -webkit-animation: anim-left 0.5s 1;
    animation: anim-left 0.5s 1;
    /*停止在最后一帧*/
    -webkit-animation-fill-mode:forwards;
    animation-fill-mode:forwards;
  }
  .white-line {
    height: 14px;
    width: 14px;
    background: url("../../../dist/assert/img/whiteLine.png") no-repeat;
    background-size: contain;
    position: absolute;
    top: 4px;
    left: 4px;
    z-index: 2;
  }
  .blue-line {
    height: 14px;
    width: 14px;
    background: url("../../../dist/assert/img/blueLine.png") no-repeat;
    background-size: contain;
    position: absolute;
    top: 4px;
    left: 4px;
    z-index: 2;
  }
  .white-pie {
    height: 14px;
    width: 14px;
    background: url("../../../dist/assert/img/whitePie.png") no-repeat;
    background-size: contain;
    position: absolute;
    top: 4px;
    right: 4px;
    z-index: 2;
  }
  .blue-pie {
    height: 14px;
    width: 14px;
    background: url("../../../dist/assert/img/bluePie.png") no-repeat;
    background-size: contain;
    position: absolute;
    top: 4px;
    right: 4px;
    z-index: 2;
  }
  .worth {
    font-size: 16px;
    height: 30px;
    line-height: 30px;
    color: #343434;
    font-weight: bold;
    font-family: monospace, serif;
  }
  .rank {
    font-size: 14px;
    height: 30px;
    line-height: 30px;
    display: flex;
    justify-content: space-between;
    padding: 3px 5px;
    color: #525252;
    background: #f8f8f8;
  }
  .rank p {
    display: inline-flex;
    align-items: center;
    justify-content: space-between;
  }
  .rank image {
    width: 18px;
    height: 18px;
    margin-right: 6px;
  }
</style>
