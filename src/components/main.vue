<template>
  <div class="hello">
    <div id="cesiumContainer"></div>

    <div class="cesium-mouse-position">
      <span>经度：</span>
      <span class="point">{{mousePosition.lng.toFixed(6)}}</span>
      <span>纬度：</span>
      <span class="point">{{mousePosition.lat.toFixed(6)}}</span>
      <span>高度：</span>
      <span class="point">{{mousePosition.height.toFixed(2)}}</span>
    </div>

    <!--功能选择-->
    <div class="operation">
      <!--图层选择-->
      <div class="operation-item operation-item-ext-imagery">
        <Dropdown trigger="hover">
          <a href="javascript:">
            <span class="change-color"><Icon type="logo-buffer" class="right-icon"/>地图图源</span>
          </a>
          <Dropdown-menu slot="list">
            <Dropdown-item>
              <a href="javascript:">谷歌图源</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">天地图</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">百度</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">高德</a>
            </Dropdown-item>
          </Dropdown-menu>
        </Dropdown>
      </div>
      <!--模型加载-->
      <div class="operation-item operation-item-ext-imagery">
        <Dropdown trigger="hover">
          <a href="javascript:">
            <span class="change-color"><Icon type="logo-buffer" class="right-icon"/>模型加载</span>
          </a>
          <Dropdown-menu slot="list">
          <Dropdown placement="right-start">
            <Dropdown-item>
              3D模型
              <Icon type="ios-arrow-forward"></Icon>
            </Dropdown-item>
            <DropdownMenu slot="list">
              <DropdownItem>人</DropdownItem>
              <Dropdown placement="right-start">
                <Dropdown-item>
                  车
                  <Icon type="ios-arrow-forward"></Icon>
                </Dropdown-item>
                <DropdownMenu slot="list">
                  <DropdownItem>静止</DropdownItem>
                  <DropdownItem>行驶</DropdownItem>
                </DropdownMenu>
              </Dropdown>
              <Dropdown placement="right-start">
                <Dropdown-item>
                  船
                  <Icon type="ios-arrow-forward"></Icon>
                </Dropdown-item>
                <DropdownMenu slot="list">
                  <DropdownItem>静止</DropdownItem>
                  <DropdownItem>行驶</DropdownItem>
                </DropdownMenu>
              </Dropdown>
              <Dropdown placement="right-start">
                <Dropdown-item>
                  飞机
                  <Icon type="ios-arrow-forward"></Icon>
                </Dropdown-item>
                <DropdownMenu slot="list">
                  <DropdownItem>静止</DropdownItem>
                  <DropdownItem>行驶</DropdownItem>
                </DropdownMenu>
              </Dropdown>
            </DropdownMenu>
          </Dropdown>
            <Dropdown-item>
              <a href="javascript:">建筑</a>
            </Dropdown-item>
          </Dropdown-menu>
        </Dropdown>
      </div>
      <!--数据加载-->
      <div class="operation-item operation-item-ext-imagery">
        <Dropdown trigger="hover">
          <a href="javascript:">
            <span class="change-color"><Icon type="logo-buffer" class="right-icon"/>数据加载</span>
          </a>
          <Dropdown-menu slot="list">
            <Dropdown-item>
              <a href="javascript:">热力图</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">迁徙图</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">雷达扫描</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">圆形扫描</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">双圆涟漪</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">闪圆</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">动态先和墙</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">道路数据</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">html元素</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">弹窗</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">动态扫描</a>
            </Dropdown-item>
          </Dropdown-menu>
        </Dropdown>
      </div>
      <!--地图操作-->
      <div class="operation-item operation-item-ext-imagery">
        <Dropdown trigger="hover">
          <a href="javascript:">
            <span class="change-color"><Icon type="logo-buffer" class="right-icon"/>地图操作</span>
          </a>
          <Dropdown-menu slot="list">
            <Dropdown-item>
              <a href="javascript:">点</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">线</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">面</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">立方体</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">测距</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">测面</a>
            </Dropdown-item>
          </Dropdown-menu>
        </Dropdown>
      </div>
      <!--图层清除-->
      <div class="operation-item operation-item-ext-imagery">
        <Dropdown trigger="hover">
          <a href="javascript:">
            <span class="change-color"><Icon type="logo-buffer" class="right-icon"/>清除</span>
          </a>
          <Dropdown-menu slot="list">
            <Dropdown-item>
              <a href="javascript:">模型</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">数据</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">绘制</a>
            </Dropdown-item>
          </Dropdown-menu>
        </Dropdown>
      </div>
    </div>
  </div>
</template>

<script>
    import '../../node_modules/cesium/Build/Cesium/Widgets/widgets.css'

    export default {
        name: 'gis',
        data() {
            return {
                viewer: '',
                mousePosition:{
                    lat:0,
                    lng:0,
                    height:0
                }
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
                    destination: new Cesium.Cartesian3.fromDegrees(114.29562, 30.58180, 1000),// eslint-disable-next-line
                    orientation: {
                        heading: Cesium.Math.toRadians(0),
                        pitch: Cesium.Math.toRadians(-61),
                        roll: 0.0
                    }
                })
                this.viewer._cesiumWidget._creditContainer.style.display = 'none'

                let me = this;
                new Cesium.ScreenSpaceEventHandler(this.viewer.canvas).setInputAction(function (e) {
                    var ellipsoid = me.viewer.scene.globe.ellipsoid
                    var cartesian = me.viewer.camera.pickEllipsoid(e.endPosition, ellipsoid)
                    var cartographic = me.viewer.scene.globe.ellipsoid.cartesianToCartographic(cartesian)
                    me.mousePosition.height = Math.ceil(me.viewer.camera.positionCartographic.height)
                    me.mousePosition.lat = Cesium.Math.toDegrees(cartographic.latitude)
                    me.mousePosition.lng = Cesium.Math.toDegrees(cartographic.longitude)
                }, Cesium.ScreenSpaceEventType.MOUSE_MOVE)
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .hello {
    height: calc(100vh - 0px);
    position: relative;
  }

  .hello #cesiumContainer {
    height: 100%;
  }

  .cesium-mouse-position {
    position: absolute;
    bottom: 0;
    width: 380px;
    padding: 0 5px;
    text-align: left;
    z-index: 1;
    background: rgba(26, 72, 126, 0.6);
    height: 22px;
    line-height: 22px;
    background: #fbfbfb;
    color: #000;
  }

  .point{
    color: #3385ff;
  }

  .operation {
    position: absolute;
    top: 20px;
    right: 20px;
    height: 45px;
    border-radius: 5px;
    line-height: 45px;
    background: #fff;
    width: auto;
  }

  .operation-item {
    display: inline-block;
    border-right: 1px dashed #dbdee2;
    height: 35px;
    line-height: 35px;
    padding: 0 5px;
  }

  .operation-item a {
    padding: 0 15px;
    color: #5f6477;
    text-decoration: none;
  }

  .right-icon {
    margin-right: 3px;
    color: #c6c0df;
    font-size: 16px;
    padding-right: 5px;
  }

  .operation-item :active, :hover, :focus {
    color: #6850d8 !important;
  }

</style>
