<template>
  <div class="wrap"
       id="scroll-wrap">
    <div id="box">
      <div id="marquee">{{text}}</div>
      <div id="copy"
           style="display: none;margin-top: -5px"></div>
    </div>
    <div id="node">{{text}}</div>
  </div>
</template>
<script type="text/ecmascript-6">
export default {
  name: 'Scroller',
  // props: ['lists'], // 父组件传入数据， 数组形式 [ "连雨不知春去"，"一晴方觉夏深"]
  props: { 'lists': { type: Array }, 'speed': { type: Number, default: 2 } },
  data () {
    return {
      text: '', // 数组文字转化后的字符串
      timer: null
    }
  },
  methods: {
    move () {
      // 获取文字text 的计算后宽度  （由于overflow的存在，直接获取不到，需要独立的node计算）
      let width = document.getElementById('node').getBoundingClientRect().width
      let box = document.getElementById('box')
      let copy = document.getElementById('copy')
      let wrapWidth = document.getElementById('scroll-wrap').getBoundingClientRect().width
      copy.innerText = this.text // 文字副本填充
      let distance = 10 // 位移距离
      let speed = this.speed
      // 设置位移
      this.timer = setInterval(function () {
        // console.log(distance)
        // console.log(width)
        distance = distance - speed
        // 如果位移超过文字宽度，则回到起点
        if (-distance >= width) {
          distance = wrapWidth
        }
        box.style.transform = 'translateX(' + distance + 'px)'
      }, 40)
    }
  },
  // 把父组件传入的arr转化成字符串
  mounted: function () {
    for (let i = 0; i < this.lists.length; i++) {
      this.text += ' ' + this.lists[i]
    }
  },
  // 更新的时候运动
  updated: function () {
    let width = document.getElementById('node').getBoundingClientRect().width
    let wrapWidth = document.getElementById('scroll-wrap').getBoundingClientRect().width
    console.log(width)
    console.log(wrapWidth)
    if (width > wrapWidth) {
      this.move()
    }
  },
  beforeDestroy () {
    window.clearInterval(this.timer);
    this.timer = null
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*样式的话可以写*/
.wrap {
  overflow: hidden;
  color: #005bbe;
}
#box {
  height: 100%;
}
#box div {
  float: left;
}
#marquee {
  margin: -5px 16px 0 20px;
  white-space: nowrap;
}
#node {
  position: absolute;
  white-space: nowrap;
  z-index: -99;
  top: -99px;
}
</style>