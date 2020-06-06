<template>
  <div style="display: flex">
    <div id="pathfinding" @mousedown.left="onMouseHold()" @mouseup.left="onMouseHold()" :style="{'gridTemplateColumns': gridStyleX, 'gridTemplateRows': gridStyleY}">
      <Block v-for="(item, i) in arrList" :key="i" @onMouseOver="onMouseOver" @onMouseClick="onMouseClick" :item="item" :index="i" :isClick="isClick" />
    </div>
    <div @click="createBox()">test</div>
  </div>
</template>

<script>
import Block from './Block'

export default {
  name: 'HelloWorld',
  components: {
    Block
  },
  data() {
    return {
      boxSizeX: 60,
      boxSizeY: 30,
      arrList: [],
      isClick: false,
    }
  },
  methods: {
    createBox() {
      this.arrList = []
      for(let i = 0; i < this.boxSizeX * this.boxSizeY; i++) {
        this.arrList.push({
          isWall: false,
          isPath: false,
          isDiscovered: false
        })
      }
    },
    onMouseHold() {
      this.isClick = !this.isClick
    },
    onMouseOver(i) {
      if(this.isClick) {
        const newObject = {...this.arrList[i]}
        newObject.isWall = !newObject.isWall
        this.$set(this.arrList, i, newObject)
      }
    },
    onMouseClick(i) {
      const newObject = {...this.arrList[i]}
      newObject.isWall = !newObject.isWall
      this.$set(this.arrList, i, newObject)
    }
  },
  computed: {
    gridStyleX() {
      const arrGrid = []
      for(let i = 0; i < this.boxSizeX; i++) {
        arrGrid.push('25px')
      }
      return (arrGrid.join(' '))
    },
    gridStyleY() {
      const arrGrid = []
      for(let i = 0; i < this.boxSizeY; i++) {
        arrGrid.push('25px')
      }
      return (arrGrid.join(' '))
    }
  },
  created() {
    this.createBox()
  }
}
</script>

<style scoped>
#pathfinding {
  width: 100vw;
  height: 100vh;
  background-color: lightblue;
  display: grid;
}
</style>
