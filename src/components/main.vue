<template>
  <div class="hello">
    <div id="cesiumContainer"></div>
  </div>
</template>

<script>
    import '../../node_modules/cesium/Build/Cesium/Widgets/widgets.css'

    export default {
        name: 'gis',
        data() {
            return {
                viewer: ''
            }
        },
        mounted() {
            this.init()
        },
        methods: {
            init() {
                var TDT_IMG_C = 'http://{s}.tianditu.gov.cn/img_c/wmts?service=wmts&request=GetTile&version=1.0.0' +
                    '&LAYER=img&tileMatrixSet=c&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}' +
                    '&style=default&format=tiles&tk=04a1ed562408cfab1fb4d6f6d3d5b77d'

                this.viewer = new Cesium.Viewer('cesiumContainer', {
                    geocoder: false, // 地理位置查询定位控件
                    homeButton: false, // 默认相机位置控件
                    timeline: false, // 时间滚动条控件
                    navigationHelpButton: false, // 默认的相机控制提示控件
                    fullscreenButton: false, // 全屏控件
                    scene3DOnly: true, // 每个几何实例仅以3D渲染以节省GPU内存
                    baseLayerPicker: false, // 底图切换控件
                    animation: false, // 控制场景动画的播放速度控件
                    infoBox: false,
                    selectionIndicator: false,
                    imageryProvider: new Cesium.WebMapTileServiceImageryProvider({
                        url: TDT_IMG_C,
                        layer: 'tdtImg_c',
                        style: 'default',
                        format: 'tiles',
                        tileMatrixSetID: 'c',
                        subdomains: ['t0', 't1', 't2', 't3', 't4', 't5', 't6', 't7'],
                        tilingScheme: new Cesium.GeographicTilingScheme(),
                        tileMatrixLabels: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19'],
                        maximumLevel: 50,
                        show: false
                    })
                })

                this.viewer.camera.setView({
                    destination: new Cesium.Cartesian3.fromDegrees(114.29562 ,30.58180, 1000),// eslint-disable-next-line
                    orientation: {
                        heading: Cesium.Math.toRadians(0),
                        pitch: Cesium.Math.toRadians(-61),
                        roll: 0.0
                    }
                })
                this.viewer._cesiumWidget._creditContainer.style.display = 'none'
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .hello{
    height: calc(100vh - 0px);
    position: relative;
  }

  .hello #cesiumContainer{
    height: 100%;
  }

</style>
