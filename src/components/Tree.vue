<template>
  <div class="tree">
    <canvas width="500" height="500" ref="tree"></canvas>
    <br>
    <br>
    <a class="save" :href="base64Image" download="code_tree.png">Save</a>
    <br>
    <br>
    <a href="#" @click.prevent="$emit('home')">Main</a>
  </div>
</template>

<script>
export default {
  name: 'tree',
  props: {
    code: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      ctx: null,
      fontSize: 14,
      lineHeight: 14,
      treeIndex: 0,
      base64Image: ''
    }
  },
  mounted () {
    this.ctx = this.$refs.tree.getContext('2d')
    this.ctx.fillStyle = '#1e1e1e'
    this.ctx.fillRect(0, 0, 500, 500)
    this.ctx.textAlign = 'center'
    this.ctx.fillStyle = 'green'
    this.ctx.font = this.fontSize + 'px consolas monospace'
    setTimeout(() => {
      this.createTree()
    }, 500)
  },
  methods: {
    createTree () {
      let x = 500 / 2
      let y = 40
      let offset = 0
      let count = 1
      let targetHeight = 30
      let i = 0
      let code = this.code

      while (code.length < 700) {
        code += code
      }

      for (i = 0; i < targetHeight; i++) {
        let targetText = code.slice(offset, offset + count)

        if (!targetText) {
          break
        }

        this.createTreeRow(
          targetText,
          x - (count * this.fontSize / 4),
          y + i * this.lineHeight
        )
        offset = offset + count
        ++count
      }

      this.createTreeStum(x, i + 2)
      this.createImage()
    },
    createTreeRow (text, x, y) {
      text.split('').forEach((c, i) => {
        const cx = x + ((i + 1) * this.fontSize / 2)
        if (Math.floor(Math.random() * 5) === 0) {
          this.createDecoration(c, cx, y)
        } else {
          this.ctx.shadowBlur = 0
          this.ctx.fillStyle = 'green'
          this.ctx.fillText(c, cx, y)
        }
      })
    },
    createDecoration (char, x, y) {
      const type = Math.floor(Math.random() * 3)

      this.ctx.shadowBlur = 7
      if (type === 0) {
        this.ctx.shadowColor = 'yellow'
        this.ctx.fillStyle = 'yellow'
      } else if (type === 1) {
        this.ctx.shadowColor = 'red'
        this.ctx.fillStyle = 'red'
      } else if (type === 2) {
        this.ctx.shadowColor = 'cyan'
        this.ctx.fillStyle = 'cyan'
      }
      this.ctx.fillText(char, x, y)
    },
    createTreeStum (x, y) {
      this.ctx.fillStyle = 'brown'
      for (let i = 0; i < 3; i++) {
        this.ctx.fillText('====',
          x,
          (y * this.lineHeight) + (this.lineHeight * i) + this.lineHeight
        )
      }
    },
    createImage () {
      this.base64Image = this.$refs.tree.toDataURL()
    }
  }
}
</script>

<style scoped lang="scss">
.tree {
  width: 100%;
  height: 100%;
  padding: 20px;
  background-color: #1e1e1e;
  color: #fff;
  text-align: center;

  canvas {
    width: 100%;
    max-width: 600px;
  }

  a {
    color: #fff;
  }

  a.save {
    color: #000;
    background-color: gold;
    box-shadow: 0 0 10px rgba(255, 215, 0, .5);
    padding: 5px 10px;
    border-radius: 5px;
  }
}
</style>
