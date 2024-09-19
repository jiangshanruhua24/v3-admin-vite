<script setup>
import BTN1 from "./Button/button1.vue"
import BTN2 from "./Button/button2.vue"
import BTN3 from "./Button/button3.vue"
import Heart from "./loadingHeart.vue"
import Line1 from "./Demo/referLine.vue"
import { ref } from "vue"
const dialogTableVisible = ref(false)
const flag = ref(0)
const openDialog = (v) => {
  dialogTableVisible.value = true
  flag.value = v
}
</script>
<template>
  <div class="btn-wrap">
    <BTN1 title="Heart" @click="openDialog(1)" />
    <BTN2 title="参考线" @click="openDialog(2)" />
    <BTN3 title="待定" @click="openDialog(3)" />
  </div>
  <el-dialog v-model="dialogTableVisible" title="View" width="80%">
    <Heart v-if="flag === 1" />
    <Line1 v-else-if="flag === 2" />
  </el-dialog>
</template>
<style scoped>
.btn-wrap {
  background-color: #ADD8E6;
  height: 100%;
}
</style>
