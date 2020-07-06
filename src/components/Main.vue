<template>
  <div class="main">
    <div class="poster">
      <img :src="image" class="original" @mousemove="moveMagnifier" @mouseleave="hideMagnifier" ref="poster">
      <div alt="" class="mag" ref="mag" v-show="hover"></div>
    </div>
    
  </div>
</template>

<script>
export default {
  name: 'Main',
  data() {
    return {
      image: "https://images.unsplash.com/photo-1573865526739-10659fec78a5?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2758&q=80",
      hover: false
    }
  },
  methods: {
    moveMagnifier(e) {
      this.hover = true

      let mag = this.$refs.mag

      mag.style.backgroundImage = "url(" + this.image + ")"

      let pos, x, y
      pos = this.cursorPosition(e)
      x = pos.x
      y = pos.y

      mag.style.backgroundPosition = '-' + x*1.8 + 'px ' + '-' + y*1.8 + 'px'

      this.$refs.mag.style.left = x - 125 + "px"
      this.$refs.mag.style.top = y - 125 + "px"
    },
    cursorPosition(e) {
      let a = this.$refs.poster.getBoundingClientRect()
      let x = e.pageX - a.left
      let y = e.pageY - a.top

      x = x - window.pageXOffset
      y = y - window.pageXOffset

      return {x : x, y : y}
    },
    hideMagnifier() {
      this.hover = false
    }
  },
}
</script>

<style scoped>

.poster {
  position:relative;
  width: 750px;
  height: 1000px;
  margin: auto;
  border: 1px solid #111;
  cursor: none;
}

.original{
  width: 750px;
  height: 1000px;
}

.mag {
  height: 250px;
  width: 250px;
  border: 5px solid #111;
  background-size: 1500px 2000px;
  background-repeat: no-repeat;
  background-color: #fff;
  position: absolute;
  pointer-events:none;
}
</style>
