<template>
  <el-container>
    <el-header>Header</el-header>
    <el-container>
      <el-aside width="200px">
        <Aside></Aside>
      </el-aside>
      <el-container>
        <el-main>
          <Map></Map>
        </el-main>
        <el-footer>Footer</el-footer>
      </el-container>
    </el-container>
  </el-container>
</template>

<script lang="ts">
import { defineComponent, onMounted, computed, ref, watch } from 'vue'
import Aside from '@/components/Aside.vue'
import Map from '@/components/Map.vue'

export default defineComponent({
  name: 'Home',
  components: {
    Aside,
    Map
  }
})
</script>

<style scoped lang="stylus">

 .el-header, .el-footer {
   background-color: #B3C0D1;
   color: #333;
   text-align: center;
   line-height: 60px;
 }

.el-aside {
  background-color: rgb(54, 61, 81);
  color: #333;
  //line-height: 200px;
  height 100%
}

.el-main {
  padding 0
}

body > .el-container {
  margin-bottom: 40px;
}

.el-container:nth-child(5) .el-aside,
.el-container:nth-child(6) .el-aside {
  line-height: 260px;
}

.el-container:nth-child(7) .el-aside {
  line-height: 320px;
}
</style>
