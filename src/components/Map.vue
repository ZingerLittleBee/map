<template>
  <div id="map-container"></div>
  <!--  <div class="input-card">-->
  <!--    <h4>聚合点效果切换</h4>-->
  <!--    <div class="input-item">-->
  <!--      <input-->
  <!--        type="button"-->
  <!--        class="btn"-->
  <!--        value="默认样式"-->
  <!--        id="add0"-->
  <!--        onclick="addCluster(0)"-->
  <!--      />-->
  <!--      <input-->
  <!--        type="button"-->
  <!--        class="btn"-->
  <!--        value="自定义图标"-->
  <!--        id="add1"-->
  <!--        onclick="addCluster(1)"-->
  <!--      />-->
  <!--      <input-->
  <!--        type="button"-->
  <!--        class="btn"-->
  <!--        value="完全自定义"-->
  <!--        id="add2"-->
  <!--        onclick="addCluster(2)"-->
  <!--      />-->
  <!--    </div>-->
  <!--  </div>-->
</template>

<script lang="ts">
import { defineComponent, onMounted } from 'vue'
import AMapLoader from '@amap/amap-jsapi-loader'
import { points } from '@/mock/points.ts'
export default defineComponent({
  name: 'Map',
  setup() {
    let map: {
      addControl: (arg0: any) => void
      add: (arg0: any) => void
      getCenter: () => any
    }
    let aMap
    onMounted(() => {
      // 加载高德地图 533351475b190d7df9bfc6a9c2ea89f2
      AMapLoader.load({
        //首次调用 load
        key: '533351475b190d7df9bfc6a9c2ea89f2', //首次load key为必填
        version: '2.0',
        plugins: ['AMap.Scale', 'AMap.ToolBar', 'AMap.MarkerCluster']
      })
        .then(AMap => {
          map = new AMap.Map('map-container')
          map.addControl(new AMap.Scale())
          map.addControl(new AMap.ToolBar())
          map.add(
            new AMap.Marker({
              position: map.getCenter()
            })
          )
          new AMap.MarkerCluster(map, points, { gridSize: 60 })
        })
        .catch(e => {
          console.error(e)
        })
    })
  }
})
</script>

<style scoped lang="stylus">
#map-container
  height 100%

.input-card {
  width: 25rem;
}

.input-card .btn {
  width: 7rem;
  margin-right: .7rem;
}

.input-card .btn:last-child {
  margin-right: 0;
}
</style>
