<template>
  <div style="display: flex; justify-content: center">
    <canvas ref="canvas" style="border: 1px solid black"></canvas>
  </div>
</template>

<script>
import { fabric } from 'fabric'
//import fs from 'fs'

export default {
  name: 'ImageEditor',
  data() {
    return {
      //
    }
  },
  mounted() {
    this.canvas = new fabric.Canvas(this.$refs.canvas, {
      enableRetinaScaling: true,
      width: 600,
      height: 600
    })
  },

  methods: {
    createRect(color) {
      const rect = new fabric.Rect({
        top: 200,
        left: 200,
        width: 50,
        height: 50,
        fill: color
      })

      this.canvas.add(rect)
    },

    createText() {
      const text = new fabric.IText('Clique e digite aqui', {
        left: 100,
        top: 100,
        fontFamily: 'sans-serif'
      })

      this.canvas.add(text)
    },

    async loadImage(imageUrl) {
      this.image = await fabric.Image.fromURL(
        imageUrl,
        (img) => {
          console.log(img)
          img.set({
            left: 50,
            top: 70,
            scaleX: 0.5,
            scaleY: 0.5,
            selectable: true,
            resizable: true
          })
          this.canvas.add(img)
          this.canvas.renderAll()
        },
        {
          crossOrigin: 'anonymous'
        }
      )
    },

    deleteSelected() {
      const selectedObject = this.canvas.getActiveObject()
      if (selectedObject) {
        this.canvas.remove(selectedObject)
      }
    },

    saveAsImage() {
      const dataUrl = this.canvas.toDataURL()

      const link = document.createElement('a')
      link.href = dataUrl

      link.download = 'spfc.png'

      document.body.appendChild(link)
      link.click()

      document.body.removeChild(link)
    },

    saveAsJSON() {
      const json = this.canvas.toJSON()
      console.log(JSON.stringify(json))
    },

    loadFromJSON(json) {
      this.canvas.loadFromJSON(json)
      this.canvas.renderAll()
    }
  }
}
</script>
