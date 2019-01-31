<template>
  <div class="aa">
    <Scroller :lists="lists"
              class="scrollContainer left" />
  </div>
</template>
<script type="text/ecmascript-6">
import Scroller from './scroll'
export default {
  components: { Scroller },

  data () {
    return {
      num: 1,
      lists: ['欢迎大家来一起学习hh,'],
    }
  }
}
</script>
<style scoped>
/*样式的话可以写*/
.scrollContainer {
  color: #ffffff;
  font-size: 16px;
  margin-left: 10px;
  width: 79%;
  height: 30px;
  line-height: 30px;
  overflow: hidden;
}
</style>