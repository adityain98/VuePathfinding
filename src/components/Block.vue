<template>
  <div class="block" :class="{'wall': item.isWall}" @mousedown.left="onMouseClick()" @mouseover="onMouseOver()">
  </div>
</template>

<script>
export default {
  methods: {
    onMouseOver() {
      this.$emit('onMouseOver', this.index)
    },
    onMouseClick() {
      this.$emit('onMouseClick', this.index)
    }
  },
  props: {
    item: Object,
    index: Number,
    isClick: Boolean
  }
}
</script>

<style scoped>

.block {
  background: white;
  border: 1px solid grey;
}

.wall {
  background-color: #0C3546;
  border: none;
  animation-name: pulse;
  animation-duration: 0.3s;
}

@keyframes pulse {
	0% {
		transform: scale(1);
    background-color: #1a6f91
	}

  50% {
    transform: scale(1.2);
    background-color: #13526b
  }

	100% {
		transform: scale(1);
    background-color: #0C3546;
	}
}

</style>