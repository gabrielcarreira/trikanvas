<template>
  <div>
    <image-editor ref="editor"></image-editor>
    <div class="button-container">
      <button
        class="button"
        @click="
          loadImage(
            'https://upload.wikimedia.org/wikipedia/pt/4/4b/S%C3%A3o_Paulo_Futebol_Clube.png'
          )
        "
      >
        SPFC
      </button>
      <div class="color-palette">
        <button
          class="color-button"
          :class="{ selected: selectedColor === '#ed2c23' }"
          @click="selectColor('#ed2c23')"
          style="background-color: #ed2c23"
        ></button>
        <button
          class="color-button"
          :class="{ selected: selectedColor === '#FFFFFF' }"
          @click="selectColor('#FFFFFF')"
          style="background-color: #ffffff"
        ></button>
        <button
          class="color-button"
          :class="{ selected: selectedColor === '#000000' }"
          @click="selectColor('#000000')"
          style="background-color: #000000"
        ></button>
      </div>
      <button class="button" @click="createRect(selectedColor)">Rect</button>
      <button class="button" @click="createText()">Text</button>
      <button class="button" @click="deleteSelected">Delete</button>
      <button class="button" @click="saveAsImage">Save</button>
    </div>
  </div>
</template>

<style>
.button-container {
  margin-top: 10px;
  display: flex;
  justify-content: center;
}

.button {
  margin-bottom: 10px;
  margin: 0 10px;
}

.color-palette {
  display: flex;
  margin-bottom: 0px;
}

.color-button {
  width: 30px;
  height: 30px;
  border: 1px solid #000;
  margin-right: 0px;
  cursor: pointer;
}

.color-button.selected {
  border: 2px solid #000;
}
</style>

<script>
import ImageEditor from './components/ImageEditor.vue'

export default {
  name: 'App',
  components: {
    ImageEditor
  },
  data() {
    return {
      selectedColor: '#000000'
    }
  },
  methods: {
    selectColor(color) {
      this.selectedColor = color
    },
    loadImage(imageUrl) {
      console.log(imageUrl)
      this.$refs.editor.loadImage(imageUrl)
    },
    createRect(color) {
      this.$refs.editor.createRect(color)
    },
    createText() {
      this.$refs.editor.createText()
    },
    deleteSelected() {
      this.$refs.editor.deleteSelected()
    },
    saveAsImage() {
      this.$refs.editor.saveAsImage()
    }
  }
}
</script>
