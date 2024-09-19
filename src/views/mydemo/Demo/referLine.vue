<script lang="ts" setup>
import { onMounted } from "vue"

onMounted(() => {
  const elements = document.querySelectorAll(".element")
  const referenceLines = document.getElementById("reference-lines")
  elements.forEach((element) => {
    element.addEventListener("mouseenter", (e) => {
      const rect = (e.target as HTMLElement).getBoundingClientRect()
      const scrollTop = window.scrollY
      const scrollLeft = window.scrollX
      console.log(scrollTop, "scrollTop")
      if (referenceLines) {
        referenceLines.innerHTML = ""
      }

      // Create horizontal top line
      const topLine = document.createElement("div")
      topLine.className = "line horizontal"
      topLine.style.top = `${rect.top}px`
      topLine.style.left = `0px`
      topLine.style.width = `${document.documentElement.clientWidth}px` // Extend across viewport width
      referenceLines.appendChild(topLine)

      // Create horizontal bottom line
      const bottomLine = document.createElement("div")
      bottomLine.className = "line horizontal"
      bottomLine.style.top = `${rect.bottom}px`
      bottomLine.style.left = `0px`
      bottomLine.style.width = `${document.documentElement.clientWidth}px` // Extend across viewport width
      referenceLines.appendChild(bottomLine)

      // Create vertical left line
      const leftLine = document.createElement("div")
      leftLine.className = "line vertical"
      leftLine.style.top = `0px`
      leftLine.style.left = `${rect.left + scrollLeft}px`
      leftLine.style.height = `${document.documentElement.clientHeight}px` // Extend across viewport height
      referenceLines.appendChild(leftLine)

      // Create vertical right line
      const rightLine = document.createElement("div")
      rightLine.className = "line vertical"
      rightLine.style.top = `0px`
      rightLine.style.left = `${rect.right + scrollLeft}px`
      rightLine.style.height = `${document.documentElement.clientHeight}px` // Extend across viewport height
      referenceLines.appendChild(rightLine)

      // Show reference lines
      referenceLines.style.display = "block"
    })

    element.addEventListener("mouseleave", () => {
      referenceLines.style.display = "none"
    })
  })
})
</script>

<template>
  <div class="container" id="container">
    <div class="element" id="element1">Element 1</div>
    <div class="element" id="element2">Element 2</div>
    <div class="element" id="element3">Element 3</div>
    <div class="element" id="element4">Element 4</div>
    <div class="element" id="element5">Element 5</div>
    <div class="element" id="element6">Element 6</div>
    <div class="element" id="element7">Element 7</div>
    <div class="element" id="element8">Element 8</div>
    <div class="element" id="element9">Element 9</div>
    <div class="element" id="element10">Element 10</div>
    <div class="reference-lines" id="reference-lines" />
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

.container {
  position: relative;
  width: 100%;
  height: 100vh;
  border: 1px solid #ccc;
  overflow: hidden;
}

.element {
  border: 1px solid #000;
  background-color: #f0f0f0;
  width: 100px;
  height: 100px;
  margin: 20px;
  display: inline-block;
  cursor: pointer;
  padding: 10px;
  border: 2px solid #ccc;
  transition:
    border-color 0.3s,
    box-shadow 0.3s;
}

.element:hover {
  box-shadow: 0 0 5px rgba(0, 0, 255, 0.5);
  /* 选中时的阴影效果 */
  outline: none;
  /* 去掉默认的焦点轮廓 */
  background-color: #ddd;
  /* 选中时的背景颜色 */
}

.reference-lines {
  position: fixed;
  pointer-events: none;
  display: none;
  z-index: 9999;
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
}

::v-deep .reference-lines .line {
  position: absolute;
  border-top: 1px dashed #00f;
  border-left: 1px dashed #00f;
  background: rgba(0, 0, 255, 0.1);
}

::v-deep .reference-lines > .horizontal {
  height: 1px;
  background: rgba(0, 0, 255, 0.2);
}

::v-deep .reference-lines > .vertical {
  width: 1px;
  background: rgba(0, 0, 255, 0.2);
}
</style>
