<template>
  <div id="map-container"></div>
  <div class="input-card">
    <h4>聚合点效果切换</h4>
    <div class="input-item">
      <input
        type="button"
        class="btn"
        value="默认样式"
        id="add0"
        onclick="addCluster(0)"
      />
      <input
        type="button"
        class="btn"
        value="自定义图标"
        id="add1"
        onclick="addCluster(1)"
      />
      <input
        type="button"
        class="btn"
        value="完全自定义"
        id="add2"
        onclick="addCluster(2)"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted } from 'vue'
import AMapLoader from '@amap/amap-jsapi-loader'
import { points } from '@/mock/points.ts'
export default defineComponent({
  name: 'Map',
  setup() {
    let map
    let aMap
    onMounted(() => {
      // 加载高德地图
      AMapLoader.load({
        key: '533351475b190d7df9bfc6a9c2ea89f2', // 申请好的Web端开发者Key，首次调用 load 时必填
        version: '2.0', // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
        plugins: ['AMap.MarkerCluster'], // 需要使用的的插件列表，如比例尺'AMap.Scale'等
        AMapUI: {
          // 是否加载 AMapUI，缺省不加载
          version: '1.1', // AMapUI 缺省 1.1
          plugins: [] // 需要加载的 AMapUI ui插件
        }
        // Loca: {
        //   // 是否加载 Loca， 缺省不加载
        //   version: '1.3.2' // Loca 版本，缺省 1.3.2
        // }
      })
        .then(AMap => {
          aMap = AMap
          map = new AMap.Map('map-container')
          const gridSize = 60
          AMap.MarkerCluster(map, points, { gridSize: gridSize })
        })
        .catch(e => {
          console.log(e)
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
