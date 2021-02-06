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

    const count = points.length

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

          const _renderClusterMarker = function(context: any) {
            const factor = Math.pow(context.count / count, 1 / 18)
            const div = document.createElement('div')
            div.style.position = 'relative'
            div.style.margin = 'auto'
            const img = document.createElement('img')
            img.src =
              'data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4NCjxzdmcgd2lkdGg9IjcycHgiIGhlaWdodD0iNzJweCIgdmlld0JveD0iMCAwIDcyIDcyIiB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiPg0KICAgIDwhLS0gR2VuZXJhdG9yOiBTa2V0Y2ggNTMuMiAoNzI2NDMpIC0gaHR0cHM6Ly9za2V0Y2hhcHAuY29tIC0tPg0KICAgIDx0aXRsZT7msJTms6E8L3RpdGxlPg0KICAgIDxkZXNjPkNyZWF0ZWQgd2l0aCBTa2V0Y2guPC9kZXNjPg0KICAgIDxkZWZzPg0KICAgICAgICA8bGluZWFyR3JhZGllbnQgeDE9IjUwJSIgeTE9IjEwMCUiIHgyPSI1MCUiIHkyPSIwJSIgaWQ9ImxpbmVhckdyYWRpZW50LTEiPg0KICAgICAgICAgICAgPHN0b3Agc3RvcC1jb2xvcj0iIzI1QzBGOCIgc3RvcC1vcGFjaXR5PSIwLjE1MzAyMzA5OCIgb2Zmc2V0PSIwJSI+PC9zdG9wPg0KICAgICAgICAgICAgPHN0b3Agc3RvcC1jb2xvcj0iIzEwOENFRSIgc3RvcC1vcGFjaXR5PSIwLjI0NTk4MDUyNSIgb2Zmc2V0PSIxMDAlIj48L3N0b3A+DQogICAgICAgIDwvbGluZWFyR3JhZGllbnQ+DQogICAgICAgIDxsaW5lYXJHcmFkaWVudCB4MT0iNTAlIiB5MT0iMTAwJSIgeDI9IjUwJSIgeTI9IjAlIiBpZD0ibGluZWFyR3JhZGllbnQtMiI+DQogICAgICAgICAgICA8c3RvcCBzdG9wLWNvbG9yPSIjMjVDMEY4IiBzdG9wLW9wYWNpdHk9IjAuMjA2MTgyMDY1IiBvZmZzZXQ9IjAlIj48L3N0b3A+DQogICAgICAgICAgICA8c3RvcCBzdG9wLWNvbG9yPSIjMTA4Q0VFIiBzdG9wLW9wYWNpdHk9IjAuMzc5ODY4NjU5IiBvZmZzZXQ9IjEwMCUiPjwvc3RvcD4NCiAgICAgICAgPC9saW5lYXJHcmFkaWVudD4NCiAgICAgICAgPGxpbmVhckdyYWRpZW50IHgxPSI1MCUiIHkxPSIxMDAlIiB4Mj0iNTAlIiB5Mj0iMCUiIGlkPSJsaW5lYXJHcmFkaWVudC0zIj4NCiAgICAgICAgICAgIDxzdG9wIHN0b3AtY29sb3I9IiMyNUMwRjgiIG9mZnNldD0iMCUiPjwvc3RvcD4NCiAgICAgICAgICAgIDxzdG9wIHN0b3AtY29sb3I9IiMxMDhDRUUiIG9mZnNldD0iMTAwJSI+PC9zdG9wPg0KICAgICAgICA8L2xpbmVhckdyYWRpZW50Pg0KICAgIDwvZGVmcz4NCiAgICA8ZyBpZD0i5L+u5pS5IiBzdHJva2U9Im5vbmUiIHN0cm9rZS13aWR0aD0iMSIgZmlsbD0ibm9uZSIgZmlsbC1ydWxlPSJldmVub2RkIj4NCiAgICAgICAgPGcgaWQ9IummlumhtTEtY29weS0yIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMjA4LjAwMDAwMCwgLTM2Ni4wMDAwMDApIj4NCiAgICAgICAgICAgIDxnIGlkPSLlsbHopb/nnIEiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIwOC4wMDAwMDAsIDM2Ni4wMDAwMDApIj4NCiAgICAgICAgICAgICAgICA8ZyBpZD0i5rCU5rOhIj4NCiAgICAgICAgICAgICAgICAgICAgPGNpcmNsZSBpZD0i5qSt5ZyG5b2iIiBmaWxsPSJ1cmwoI2xpbmVhckdyYWRpZW50LTEpIiBjeD0iMzYiIGN5PSIzNiIgcj0iMzYiPjwvY2lyY2xlPg0KICAgICAgICAgICAgICAgICAgICA8Y2lyY2xlIGlkPSLmpK3lnIblvaIiIGZpbGw9InVybCgjbGluZWFyR3JhZGllbnQtMikiIGN4PSIzNi41IiBjeT0iMzUiIHI9IjMwLjUiPjwvY2lyY2xlPg0KICAgICAgICAgICAgICAgICAgICA8Y2lyY2xlIGlkPSLmpK3lnIblvaIiIGZpbGw9InVybCgjbGluZWFyR3JhZGllbnQtMykiIGN4PSIzNiIgY3k9IjM2IiByPSIyNCI+PC9jaXJjbGU+DQogICAgICAgICAgICAgICAgPC9nPg0KICAgICAgICAgICAgPC9nPg0KICAgICAgICA8L2c+DQogICAgPC9nPg0KPC9zdmc+'
            const Hue = 180 - factor * 180
            // const bgColor = 'hsla(' + Hue + ',100%,40%,0.7)'
            // const fontColor = 'hsla(' + Hue + ',100%,90%,1)'
            // const borderColor = 'hsla(' + Hue + ',100%,40%,1)'
            // const shadowColor = 'hsla(' + Hue + ',100%,90%,1)'
            // div.style.backgroundColor = 'black'
            const size = Math.round(
              30 + Math.pow(context.count / count, 1 / 5) * 20
            )
            div.style.width = div.style.height = img.style.width = img.style.height =
              size + 'px'
            // div.style.border = 'solid 1px ' + borderColor
            div.style.borderRadius = size / 2 + 'px'
            // div.style.boxShadow = '0 0 5px ' + shadowColor
            // div.innerHTML = context.count
            // div.style.lineHeight = size + 'px'
            // div.style.color = fontColor
            // div.style.fontSize = '14px'
            // div.style.textAlign = 'center'
            const span = document.createElement('div')

            span.innerHTML = context.count
            span.style.position = 'absolute'
            span.style.top = span.style.left = span.style.right = span.style.bottom =
              '0'
            span.style.textAlign = 'center'
            span.style.lineHeight = `${size}px`
            span.style.fontSize = '14px'
            span.style.color = '#fff'

            // 动画
            const animation1 = document.createElement('div')
            // animation1.style.animation = 'ring 3s linear 2s infinite'
            animation1.animate(
              [{ opacity: 0 }, { opacity: 1, offset: 0.4 }, { opacity: 0 }],
              {
                duration: 3000,
                fill: 'forwards',
                easing: 'steps(8, end)',
                iterations: Infinity
              }
            )

            div.appendChild(img)
            div.appendChild(span)
            div.appendChild(animation1)
            context.marker.setOffset(new AMap.Pixel(-size / 2, -size / 2))
            context.marker.setContent(div)
          }

          const MarkerClusterOptions = {
            gridSize: 200,
            clusterByZoomChange: true,
            maxZoom: 12,
            renderClusterMarker: _renderClusterMarker
          }
          new AMap.MarkerCluster(map, points, MarkerClusterOptions)
        })
        .catch(e => {
          console.error(e)
        })
    })
  }
})
</script>

<style lang="stylus">
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

@-webkit-keyframes ring {
  0% {
    -webkit-transform: scale(0.6);
    transform: scale(0.6);
    opacity: 0.6;
  }
  80% {
    -webkit-transform: scale(1.3);
    transform: scale(1.3);
    opacity: 0.5;
  }
  to {
    -webkit-transform: scale(1.4);
    transform: scale(1.4);
    opacity: 0;
  }
}
@keyframes ring {
  0% {
    -webkit-transform: scale(0.6);
    transform: scale(0.6);
    opacity: 0.6;
  }
  80% {
    -webkit-transform: scale(1.3);
    transform: scale(1.3);
    opacity: 0.5;
  }
  to {
    -webkit-transform: scale(1.4);
    transform: scale(1.4);
    opacity: 0;
  }
}
</style>
