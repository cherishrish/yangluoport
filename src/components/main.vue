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
              <a href="javascript:">动态线和墙</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">道路数据</a>npm
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
              <a href="javascript:" @click="draw_picture(1)">点</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="draw_picture(2)">线</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="draw_picture(3)">面</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="draw_picture(4)">立方体</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="draw_picture(5)">测距</a>
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
              <a href="javascript:" @click="clearDrawingBoard">绘制</a>
            </Dropdown-item>
          </Dropdown-menu>
        </Dropdown>
      </div>
    </div>
  </div>
</template>

<script>
  import '../../node_modules/cesium/Build/Cesium/Widgets/widgets.css'
  import Drop from "view-design/src/components/select/dropdown";

  export default {
    name: 'gis',
    components: {Drop},
    data() {
      return {
        viewer: '',
        // draw:false,
        mousePosition: {
          lat: 0,
          lng: 0,
          height: 0
        },
        activeShapePoints: [],//点集合
        activeShape: '',
        floatingPoint: null,//矩形中的标识点
        draw: false,//是否绘制
        latObj: '',//定点位置信息
        drawingMode: '',//绘制类型
        lastPosition: null,//设置前一个点
        menu: document.getElementById("menu"),//获取右键菜单
        begin: false,//是否开始绘制
        tempEntities: [],//实体列表,= entities_point
        count: 1,//点的数量
        buildLine: null,//开启测距
        buildArea: null,//开启测面
        linePoint: null,//终点实体
        right: null,//终点坐标
        rec: false,//开启绘制矩形
        rectangle: null,//矩形实体
        recPoints: [],//矩形点的集合
        num: 0,
        polyline: null,//活动线
        polylineData: null,//线数据
        polylineLast: null,//最后的线数据
        Entities_line: [],//脏数据
        polygon: null, // 活动面
        polygonData: null, //面数据
        polygonLast: null, // 最后的面数据
        Entities_polygon: [],//脏数据
        handler: '',
        draw_able: false,//是否开始画
        index: 1,
        line_able:false,//是否画线
        polygon_able: false,//是否画面
        rectangle_able:false,//是否画矩形
        rectangle:null,//矩形
        getDistance_able:false,//是否测距
        // pointData:[],
        // pointArrays:[],
        // lineArrays:[],
        // lineEntity:{},
        // polygonEntity:{},
        // showPointAlert:false,
      }
    },
    mounted() {
      this.init();
      //双击鼠标清除默认事件
      // this.viewer._cesiumWidget.screenSpaceEventHandler.removeInputAction(Cesium.ScreenSpaceEventType.LEFT_DOUBLE_CLICK);
    },
    methods: {
      draw_picture(index) {
        this.draw_able = true
        var me = this
        if (index === 1) {
          this.index = 1
        }
        else if (index === 2) {
          this.draw_able = true
          this.line_able = true
          this.index = 2
        }
        else if (index === 3){
          this.draw_able = true
          this.polygon_able = true
          this.index = 3
        }
        else if (index === 4){
          this.draw_able = true
          this.rectangle_able = true
          this.index = 4
        }
        else if (index === 5){
          this.draw_able = true
          this.getDistance_able = true
          this.index = 5
        }
        this.handler.setInputAction(function (e) {
          me.draw_able = false
          me.line_able = false
          me.polygon_able = false
          me.rectangle_able = false
          me.getDistance_able = false
          me.activeShapePoints = []
        }, Cesium.ScreenSpaceEventType.RIGHT_CLICK);

      },
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
        this.viewer._cesiumWidget._creditContainer.style.display = 'none';

        this.handler = new Cesium.ScreenSpaceEventHandler(this.viewer.canvas);

        let me = this;
        new Cesium.ScreenSpaceEventHandler(this.viewer.canvas).setInputAction(function (e) {
          var ellipsoid = me.viewer.scene.globe.ellipsoid
          var cartesian = me.viewer.camera.pickEllipsoid(e.endPosition, ellipsoid)
          var cartographic = me.viewer.scene.globe.ellipsoid.cartesianToCartographic(cartesian)
          me.mousePosition.height = Math.ceil(me.viewer.camera.positionCartographic.height)
          me.mousePosition.lat = Cesium.Math.toDegrees(cartographic.latitude)
          me.mousePosition.lng = Cesium.Math.toDegrees(cartographic.longitude)
          if(me.line_able){
            if (me.activeShapePoints.length < 1) return;
            var cartesian = me.viewer.scene.camera.pickEllipsoid(e.endPosition);
            if (!Cesium.defined(me.polyline)) {
              me.polyline = me.createPolyline()//画线
            }
            if (me.polyline) {
              me.polyline.pop();
              me.polyline.push(cartesian);
            }
          }
          else if(me.polygon_able){//面
            if (me.activeShapePoints.length < 1) return;
            var cartesian = me.viewer.camera.pickEllipsoid(e.endPosition);
            if (me.activeShapePoints.length >= 3) {//当所画的点的个数大于等于3画面
              if (!Cesium.defined(me.polygon)) {
                me.polygon = me.createPolygon();
              }
            }
            me.activeShapePoints.pop();
            me.activeShapePoints.push(cartesian);
          }
          else if(me.rectangle_able){//矩形
            if (me.activeShapePoints.length < 3) return;
            var cartesian = me.viewer.camera.pickEllipsoid(e.endPosition);
            if (!Cesium.defined(me.rectangle)) {
              me.rectangle = me.createRectangle();
            }
//            me.floatingPoint.endPosition.setValue(cartesian);//endPosition未定义
            if (me.rectangle) {
              me.activeShapePoints.pop();
              me.activeShapePoints.push(cartesian);
            }
          }
          else if(me.getDistance_able){//测距,这一部分与画线的右击重复
            if (me.activeShapePoints.length < 1) return;
            var cartesian = me.viewer.scene.camera.pickEllipsoid(e.endPosition);
            if (!Cesium.defined(me.polyline)) {
              me.polyline = me.createPolyline()//画线
            }
            if (me.polyline) {
              me.polyline.pop();
              me.polyline.push(cartesian);
            }
          }

        }, Cesium.ScreenSpaceEventType.MOUSE_MOVE);

        this.handler.setInputAction(function (e) { //单击开始绘制
          if (me.draw_able) {
            if (me.index === 1) {
              me.createPoint(e)
            } else if (me.index === 2) {//绘制线左键单击
              var cartesian = me.viewer.scene.camera.pickEllipsoid(e.position, me.viewer.scene.globe.ellipsoid);
              if (me.activeShapePoints.length === 0) {
                me.activeShapePoints.push(cartesian.clone());
              }
              me.activeShapePoints.push(cartesian);
              me.createPoint(e);// 绘制点
            } else if (me.index === 3) {//绘制面左键单击
              var cartesian = me.viewer.scene.camera.pickEllipsoid(e.position, me.viewer.scene.globe.ellipsoid);
              if (me.activeShapePoints == 0) {
                me.activeShapePoints.push(cartesian.clone());
              }
              me.createPoint(e);//产生点
              me.activeShapePoints.push(cartesian);
            }
            else if(me.index === 4){//绘制矩形左键单击
              var cartesian = me.viewer.scene.camera.pickEllipsoid(e.position, me.viewer.scene.globe.ellipsoid);
              if (me.activeShapePoints == 0) {
                me.activeShapePoints.push(cartesian.clone());
              }
              me.createPoint(e);//产生点
              me.floatingPoint = me.createPoint(e);
              me.activeShapePoints.push(cartesian);
            }
            else if(me.index === 5){//测距单击
              var cartesian = me.viewer.scene.camera.pickEllipsoid(e.position, me.viewer.scene.globe.ellipsoid);
              if (me.activeShapePoints == 0) {
                me.activeShapePoints.push(cartesian.clone());
              }
              me.activeShapePoints.push(cartesian);
              var text="起点";
              if(me.polyline){
                text = me.getSpaceDistance(me.activeShapePoints);
              }
              me.createPoint2(e,text);// 绘制点
            }
          }
        }, Cesium.ScreenSpaceEventType.LEFT_CLICK);
      },
      //画点
      createPoint(e) {
        var _this = this;
        var cartesian = _this.viewer.scene.camera.pickEllipsoid(e.position, _this.viewer.scene.globe.ellipsoid);
        var point = _this.viewer.entities.add({
          position: cartesian,
          point: {
            color: Cesium.Color.RED,
            pixelSize: 8,
            heightReference: Cesium.HeightReference.CLAMP_TO_GROUND
          },
        });
      },

      //创建线
      createPolyline() {
        var $this = this;
        var polyline = $this.viewer.entities.add({
          polyline: {
            positions: $this.activeShapePoints,
            show: true,
            material: Cesium.Color.RED,
            width: 3,
            clampToGround: true
          }
        });
        $this.Entities_line.push(polyline);
      },

      //创建面
      createPolygon(){
        var $this = this;
        var polygon = $this.viewer.entities.add({
          polygon: {
            // hierarchy: $this.activeShapePoints,//位置可能出现问题
            // clampToGround: true,
            // show: true,
            // fill: true,
            // material: Cesium.Color.RED.withAlpha(0.5),
            // width: 3,
            // outlineColor: Cesium.Color.BLACK,
            // outlineWidth: 1,
            // outline: false
            hierarchy: new Cesium.PolygonHierarchy($this.activeShapePoints),
            material: new Cesium.ColorMaterialProperty(Cesium.Color.BLUE.withAlpha(0.5))
          }
        });
        $this.tempEntities.push(polygon);//储存脏数据
      },

       //  立方体
      createRectangle() {
        var $this = this;
        var rectangle = $this.viewer.entities.add({
//          name: "rectangle",
          rectangle: {
            coordinates: new Cesium.Rectangle.fromCartesianArray($this.activeShapePoints),
            material: Cesium.Color.RED.withAlpha(0.5)
          }
        });
        $this.tempEntities.push(rectangle);
      },

       //  测距
      //测距产生的点
      createPoint2(e,text) {
        var _this = this;
        var cartesian = _this.viewer.scene.camera.pickEllipsoid(e.position, _this.viewer.scene.globe.ellipsoid);
        var point = _this.viewer.entities.add({
          position: cartesian,
          point: {
            color: Cesium.Color.RED,
            pixelSize: 8,
            heightReference: Cesium.HeightReference.CLAMP_TO_GROUND
          },
          label: {
            text: text,
            font: '18px sans-serif',
            style : Cesium.LabelStyle.FILL,
            outlineWidth : 1,
            fillColor: Cesium.Color.WHITE,
            showBackground:false,
            backgroundColor: Cesium.Color.ORANGE.withAlpha(0.6),
            horizontalOrigin: Cesium.HorizontalOrigin.LEFT,
            pixelOffset: new Cesium.Cartesian2(5.0,-20.0),
          }
        });
      },
      getSpaceDistance(positions) {
        var distance = 0;
        var $this=this;
        for (var i = 0; i < positions.length - 1; i++) {
          var point1cartographic = $this.Cesium.Cartographic.fromCartesian(positions[i]);
          var point2cartographic = $this.Cesium.Cartographic.fromCartesian(positions[i + 1]);
          /**根据经纬度计算出距离**/
          var geodesic = new $this.Cesium.EllipsoidGeodesic();
          geodesic.setEndPoints(point1cartographic, point2cartographic);
          var s = geodesic.surfaceDistance;
          //console.log(Math.sqrt(Math.pow(distance, 2) + Math.pow(endheight, 2)));
          //返回两点之间的距离
          s = Math.sqrt(Math.pow(s, 2) + Math.pow(point2cartographic.height - point1cartographic.height, 2));
          distance = distance + s;
        }
        return distance.toFixed(2)>1000 ? (distance/1000).toFixed(2)+"公里" : distance.toFixed(2)+"米";
      },
       //  测面
       //  清除
      clearDrawingBoard() {
        this.viewer.entities.removeAll();//删除全部
        // var me = this;
        // var primitives = me.viewer.entities;
        // for (var i = 0; i <  me.tempEntities.length; i++) {
        //   primitives.remove(me.tempEntities[i]);
        // }
        // me.tempEntities=[];
      },
      //
      // /**清除实体*/
      // terminateShape(){
      //   var $this = this;
      //   $this.activeShapePoints.pop();//去除最后一个动态点
      //   if($this.activeShapePoints.length){
      //     // $this.drawShape($this.activeShapePoints);//绘制最终图的代码需要修改
      //
      //   }
      //   $this.viewer.entities.remove($this.floatingPoint); //去除动态点图形（当前鼠标点）
      //   $this.viewer.entities.remove($this.activeShape); //去除动态图形
      //   $this.floatingPoint = undefined;
      //   $this.activeShape = undefined;
      //   $this.activeShapePoints = [];
      // }


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

  .point {
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
