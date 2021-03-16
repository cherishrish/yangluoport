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
              <a href="javascript:" @click="showRadarScan">雷达扫描</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="showCircleScan">圆形扫描</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="showDoubleCircleWave">双圆涟漪</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="flashRound">闪点</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="flashCircle">闪圆</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="addLine">动态线和墙</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:">道路数据</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="addHtml">html元素</a>
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
              <a href="javascript:" @click="draw_picture(4)">矩形</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="draw_picture(5)">测距</a>
            </Dropdown-item>
            <Dropdown-item>
              <a href="javascript:" @click="draw_picture(6)">测面</a>
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
        mousePosition: {
          lat: 0,
          lng: 0,
          height: 0
        },
        activeShapePoints: [],//点集合
        floatingPoint: null,//矩形中的标识点,面
        rectangle: null,//矩形实体
        num: 0,
        polyline: null,//活动线
        polylinePoint: null,//线数据
        polylineLastPoint: null,//线上的最终点
        lastPosition: null,//上一个点
        linePositionData: [],//线上的点数据，用于显示距离数据
        polygon: null, // 活动面
        polygonData: null, //面数据
        handler: '',//鼠标事件
        draw_able: false,//是否开始画
        index: 1,
        line_able: false,//是否画线
        polygon_able: false,//是否画面
        rectangle_able: false,//是否画矩形
        rectangle: null,//矩形
        getDistance_able: false,//是否测距
        line_text: null,//存放距离
        count: 1,//点的数量
        distance: 0,//距离 暂时没用到
        getArea_able: false,//是否测面
        polygonCenter: 0,//面的中心
        polylineCenyer: 0,//线段的中心
//        测面过程中需要声明的全局变量
        earthRadiusMeters: 6371000.0,
        radiansPerDegree: Math.PI / 180.0,
        degreesPerRadian: 180.0 / Math.PI,
        text: null,//需要显示的文字,
        radarsScans: [],
        //双圆涟漪的data
        data: {
          id: "[1,2]",
          lon: 114.292832,
          lat: 30.584519,
          height: 500,
          maxR: 3000,
          minR: 0,//最好为0
          deviationR: 10,//差值 差值也大 速度越快
          eachInterval: 2000,//两个圈的时间间隔
          imageUrl: "../../static/redCircle.png"//波纹图片
        }
      }
    },
    mounted() {
      this.init();
    },
    methods: {
      //双圆涟漪
      showDoubleCircleWave() {//扩散效果
        var _this = this
        //添加中心线
        _this.viewer.entities.add({
          name: "中心线",
          polyline: {
            positions: Cesium.Cartesian3.fromDegreesArrayHeights([
              _this.data.lon, _this.data.lat, 0,
              _this.data.lon, _this.data.lat, 5000,]//中心线的高度
            ),
            width: 4,
            material: new Cesium.PolylineGlowMaterialProperty({ //发光线
              glowPower: 0.1,
              color: Cesium.Color.RED
            })
          }
        });
        var r1 = _this.data.minR, r2 = _this.data.minR;

        function changeR1() { //这是callback，参数不能内传
          r1 = r1 + _this.data.deviationR;
          if (r1 >= _this.data.maxR) {
            r1 = _this.data.minR;
          }
          return r1;
        }//通过改变圆的大小来实现波纹效果

        function changeR2() {
          r2 = r2 + _this.data.deviationR;
          if (r2 >= _this.data.maxR) {
            r2 = _this.data.minR;
          }
          return r2;
        }//通过改变圆的大小来实现波纹效果

        _this.viewer.entities.add({
          id: _this.data.id,
          name: "",
          position: Cesium.Cartesian3.fromDegrees(_this.data.lon, _this.data.lat, _this.data.height),
          ellipse: {
            semiMinorAxis: new Cesium.CallbackProperty(changeR1, false),
            semiMajorAxis: new Cesium.CallbackProperty(changeR1, false),
            height: _this.data.height,
            material: new Cesium.ImageMaterialProperty({
              image: _this.data.imageUrl,
              repeat: new Cesium.Cartesian2(1.0, 1.0),
              transparent: true,
              color: new Cesium.CallbackProperty(function () {
                var alp = 1 - r1 / _this.data.maxR;
                return Cesium.Color.WHITE.withAlpha(alp)  //entity的颜色透明 并不影响材质，并且 entity也会透明哦
              }, false)
            })
          }
        });
        //延时效果
        setTimeout(function () {
          //第二个圆开始跑
          _this.viewer.entities.add({
            name: "",
            position: Cesium.Cartesian3.fromDegrees(_this.data.lon, _this.data.lat, _this.data.height),
            ellipse: {
              semiMinorAxis: new Cesium.CallbackProperty(changeR2, false),
              semiMajorAxis: new Cesium.CallbackProperty(changeR2, false),
              height: _this.data.height,
              material: new Cesium.ImageMaterialProperty({
                image: _this.data.imageUrl,
                repeat: new Cesium.Cartesian2(1.0, 1.0),
                transparent: true,
                color: new Cesium.CallbackProperty(function () {
                  var alp = 1;
                  alp = 1 - r2 / _this.data.maxR;
                  return Cesium.Color.WHITE.withAlpha(alp)
                }, false)
              })
            }
          });
        }, _this.data.eachInterval)
      },
      //实现动态线和墙
      //添加静态的线
      addLine() {
        var _this = this;
        var addline = _this.viewer.entities.add({
          polyline: {
            positions: Cesium.Cartesian3.fromDegreesArrayHeights( [
              114.292832, 30.584519,0, //0 表示高度
              114.292832 + 1, 30.584519, 0,
              114.292832 + 1, 30.584519 + 1, 0,
              114.292832 + 2, 30.584519+1, 0,
              114.292832 + 2, 30.584519 + 2, 0
              ],),
              width:5,
              clampToGround : true,//贴地
              material: Cesium.Color.RED,
          }
        });
      },
      //添加Html
      addHtml(){
        // var _this = this
        // _this.viewer.entities.add({
        //   html: {
        //     position: [114.292832, 30.584519, 20],
        //     element: `<div class="html-box">2</div>`,
        //     offset: [10, 10]
        //   }
        // });
      },
      //实现雷达效果
      showRadarScan() {
        let _this = this
        var cartographicCenter = new Cesium.Cartographic(Cesium.Math.toRadians(114.292832), Cesium.Math.toRadians(30.584519), 32);//添加雷达扫描效果的点
        var scanColor = new Cesium.Color(1.0, 0.0, 0.0, 1);

        var lastStage = _this.addRadarScanPostStage(_this.viewer, cartographicCenter, 1000, scanColor, 3000);
      },
      /*
       添加扩散效果扫描线
       viewer
       cartographicCenter 扫描中心
       radius  半径 米
       scanColor 扫描颜色
       duration 持续时间 毫秒
       */
      addRadarScanPostStage(viewer, cartographicCenter, radius, scanColor, duration) {
        let _this = this
        var _Cartesian3Center = Cesium.Cartographic.toCartesian(cartographicCenter);
        var _Cartesian4Center = new Cesium.Cartesian4(_Cartesian3Center.x, _Cartesian3Center.y, _Cartesian3Center.z, 1);

        var _CartographicCenter1 = new Cesium.Cartographic(cartographicCenter.longitude, cartographicCenter.latitude, cartographicCenter.height + 500);
        var _Cartesian3Center1 = Cesium.Cartographic.toCartesian(_CartographicCenter1);
        var _Cartesian4Center1 = new Cesium.Cartesian4(_Cartesian3Center1.x, _Cartesian3Center1.y, _Cartesian3Center1.z, 1);

        var _CartographicCenter2 = new Cesium.Cartographic(cartographicCenter.longitude + Cesium.Math.toRadians(0.001), cartographicCenter.latitude, cartographicCenter.height);
        var _Cartesian3Center2 = Cesium.Cartographic.toCartesian(_CartographicCenter2);
        var _Cartesian4Center2 = new Cesium.Cartesian4(_Cartesian3Center2.x, _Cartesian3Center2.y, _Cartesian3Center2.z, 1);
        var _RotateQ = new Cesium.Quaternion();
        var _RotateM = new Cesium.Matrix3();

        var _time = (new Date()).getTime();

        var _scratchCartesian4Center = new Cesium.Cartesian4();
        var _scratchCartesian4Center1 = new Cesium.Cartesian4();
        var _scratchCartesian4Center2 = new Cesium.Cartesian4();
        var _scratchCartesian3Normal = new Cesium.Cartesian3();
        var _scratchCartesian3Normal1 = new Cesium.Cartesian3();

        var ScanPostStage = new Cesium.PostProcessStage({
          fragmentShader: _this.getRadarScanShader(),
          uniforms: {
            u_scanCenterEC: function () {
              return Cesium.Matrix4.multiplyByVector(viewer.camera._viewMatrix, _Cartesian4Center, _scratchCartesian4Center);
            },
            u_scanPlaneNormalEC: function () {
              var temp = Cesium.Matrix4.multiplyByVector(viewer.camera._viewMatrix, _Cartesian4Center, _scratchCartesian4Center);
              var temp1 = Cesium.Matrix4.multiplyByVector(viewer.camera._viewMatrix, _Cartesian4Center1, _scratchCartesian4Center1);
              _scratchCartesian3Normal.x = temp1.x - temp.x;
              _scratchCartesian3Normal.y = temp1.y - temp.y;
              _scratchCartesian3Normal.z = temp1.z - temp.z;

              Cesium.Cartesian3.normalize(_scratchCartesian3Normal, _scratchCartesian3Normal);
              return _scratchCartesian3Normal;
            },
            u_radius: radius,
            u_scanLineNormalEC: function () {
              var temp = Cesium.Matrix4.multiplyByVector(viewer.camera._viewMatrix, _Cartesian4Center, _scratchCartesian4Center);
              var temp1 = Cesium.Matrix4.multiplyByVector(viewer.camera._viewMatrix, _Cartesian4Center1, _scratchCartesian4Center1);
              var temp2 = Cesium.Matrix4.multiplyByVector(viewer.camera._viewMatrix, _Cartesian4Center2, _scratchCartesian4Center2);

              _scratchCartesian3Normal.x = temp1.x - temp.x;
              _scratchCartesian3Normal.y = temp1.y - temp.y;
              _scratchCartesian3Normal.z = temp1.z - temp.z;

              Cesium.Cartesian3.normalize(_scratchCartesian3Normal, _scratchCartesian3Normal);

              _scratchCartesian3Normal1.x = temp2.x - temp.x;
              _scratchCartesian3Normal1.y = temp2.y - temp.y;
              _scratchCartesian3Normal1.z = temp2.z - temp.z;

              var tempTime = (((new Date()).getTime() - _time) % duration) / duration;
              Cesium.Quaternion.fromAxisAngle(_scratchCartesian3Normal, tempTime * Cesium.Math.PI * 2, _RotateQ);
              Cesium.Matrix3.fromQuaternion(_RotateQ, _RotateM);
              Cesium.Matrix3.multiplyByVector(_RotateM, _scratchCartesian3Normal1, _scratchCartesian3Normal1);
              Cesium.Cartesian3.normalize(_scratchCartesian3Normal1, _scratchCartesian3Normal1);
              return _scratchCartesian3Normal1;
            },
            u_scanColor: scanColor
          }
        });
        _this.viewer.scene.postProcessStages.add(ScanPostStage);

        return ScanPostStage;
      },

      //雷达扫描线效果Shader
      getRadarScanShader() {
        var _this = this
        var scanSegmentShader =
          "uniform sampler2D colorTexture;\n" +
          "uniform sampler2D depthTexture;\n" +
          "varying vec2 v_textureCoordinates;\n" +
          "uniform vec4 u_scanCenterEC;\n" +
          "uniform vec3 u_scanPlaneNormalEC;\n" +
          "uniform vec3 u_scanLineNormalEC;\n" +
          "uniform float u_radius;\n" +
          "uniform vec4 u_scanColor;\n" +

          "vec4 toEye(in vec2 uv, in float depth)\n" +
          " {\n" +
          " vec2 xy = vec2((uv.x * 2.0 - 1.0),(uv.y * 2.0 - 1.0));\n" +
          " vec4 posInCamera =czm_inverseProjection * vec4(xy, depth, 1.0);\n" +
          " posInCamera =posInCamera / posInCamera.w;\n" +
          " return posInCamera;\n" +
          " }\n" +

          "bool isPointOnLineRight(in vec3 ptOnLine, in vec3 lineNormal, in vec3 testPt)\n" +
          "{\n" +
          "vec3 v01 = testPt - ptOnLine;\n" +
          "normalize(v01);\n" +
          "vec3 temp = cross(v01, lineNormal);\n" +
          "float d = dot(temp, u_scanPlaneNormalEC);\n" +
          "return d > 0.5;\n" +
          "}\n" +

          "vec3 pointProjectOnPlane(in vec3 planeNormal, in vec3 planeOrigin, in vec3 point)\n" +
          "{\n" +
          "vec3 v01 = point -planeOrigin;\n" +
          "float d = dot(planeNormal, v01) ;\n" +
          "return (point - planeNormal * d);\n" +
          "}\n" +

          "float distancePointToLine(in vec3 ptOnLine, in vec3 lineNormal, in vec3 testPt)\n" +
          "{\n" +
          "vec3 tempPt = pointProjectOnPlane(lineNormal, ptOnLine, testPt);\n" +
          "return length(tempPt - ptOnLine);\n" +
          "}\n" +

          "float getDepth(in vec4 depth)\n" +
          "{\n" +
          "float z_window = czm_unpackDepth(depth);\n" +
          "z_window = czm_reverseLogDepth(z_window);\n" +
          "float n_range = czm_depthRange.near;\n" +
          "float f_range = czm_depthRange.far;\n" +
          "return (2.0 * z_window - n_range - f_range) / (f_range - n_range);\n" +
          "}\n" +

          "void main()\n" +
          "{\n" +
          "gl_FragColor = texture2D(colorTexture, v_textureCoordinates);\n" +
          "float depth = getDepth( texture2D(depthTexture, v_textureCoordinates));\n" +
          "vec4 viewPos = toEye(v_textureCoordinates, depth);\n" +
          "vec3 prjOnPlane = pointProjectOnPlane(u_scanPlaneNormalEC.xyz, u_scanCenterEC.xyz, viewPos.xyz);\n" +
          "float dis = length(prjOnPlane.xyz - u_scanCenterEC.xyz);\n" +
          "float twou_radius = u_radius * 2.0;\n" +
          "if(dis < u_radius)\n" +
          "{\n" +
          "float f0 = 1.0 -abs(u_radius - dis) / u_radius;\n" +
          "f0 = pow(f0, 64.0);\n" +
          "vec3 lineEndPt = vec3(u_scanCenterEC.xyz) + u_scanLineNormalEC * u_radius;\n" +
          "float f = 0.0;\n" +
          "if(isPointOnLineRight(u_scanCenterEC.xyz, u_scanLineNormalEC.xyz, prjOnPlane.xyz))\n" +
          "{\n" +
          "float dis1= length(prjOnPlane.xyz - lineEndPt);\n" +
          "f = abs(twou_radius -dis1) / twou_radius;\n" +
          "f = pow(f, 3.0);\n" +
          "}\n" +
          "gl_FragColor = mix(gl_FragColor, u_scanColor, f + f0);\n" +
          "}\n" +
          "}\n";
        return scanSegmentShader;
      },
      //圆形扫描
      showCircleScan() {
        let _this = this
        var cartographicCenter = new Cesium.Cartographic(Cesium.Math.toRadians(114.292832), Cesium.Math.toRadians(30.584519), 32);
        var scanColor = new Cesium.Color(0.0, 1.0, 0.0, 1);
        var lastStage = _this.addCircleScanPostStage(_this.viewer, cartographicCenter, 1000, scanColor, 4000);
      },
      //添加圆形扫描线
      addCircleScanPostStage(viewer, cartographicCenter, maxRadius, scanColor, duration) {
        let _this = this
        var _Cartesian3Center = Cesium.Cartographic.toCartesian(cartographicCenter);
        var _Cartesian4Center = new Cesium.Cartesian4(_Cartesian3Center.x, _Cartesian3Center.y, _Cartesian3Center.z, 1);

        var _CartograhpicCenter1 = new Cesium.Cartographic(cartographicCenter.longitude, cartographicCenter.latitude, cartographicCenter.height + 500);
        var _Cartesian3Center1 = Cesium.Cartographic.toCartesian(_CartograhpicCenter1);
        var _Cartesian4Center1 = new Cesium.Cartesian4(_Cartesian3Center1.x, _Cartesian3Center1.y, _Cartesian3Center1.z, 1);

        var _time = (new Date()).getTime();

        var _scratchCartesian4Center = new Cesium.Cartesian4();
        var _scratchCartesian4Center1 = new Cesium.Cartesian4();
        var _scratchCartesian3Normal = new Cesium.Cartesian3();


        var ScanPostStage = new Cesium.PostProcessStage({
          fragmentShader: _this.getScanSegmentShader(),
          uniforms: {
            u_scanCenterEC: function () {
              var temp = Cesium.Matrix4.multiplyByVector(viewer.camera._viewMatrix, _Cartesian4Center, _scratchCartesian4Center);
              return temp;
            },
            u_scanPlaneNormalEC: function () {
              var temp = Cesium.Matrix4.multiplyByVector(viewer.camera._viewMatrix, _Cartesian4Center, _scratchCartesian4Center);
              var temp1 = Cesium.Matrix4.multiplyByVector(viewer.camera._viewMatrix, _Cartesian4Center1, _scratchCartesian4Center1);

              _scratchCartesian3Normal.x = temp1.x - temp.x;
              _scratchCartesian3Normal.y = temp1.y - temp.y;
              _scratchCartesian3Normal.z = temp1.z - temp.z;

              Cesium.Cartesian3.normalize(_scratchCartesian3Normal, _scratchCartesian3Normal);

              return _scratchCartesian3Normal;
            },
            u_radius: function () {
              return maxRadius * (((new Date()).getTime() - _time) % duration) / duration;
            },
            u_scanColor: scanColor
          }
        });

        _this.viewer.scene.postProcessStages.add(ScanPostStage);
        return ScanPostStage;
      },
      //扩散效果Shader
      /*
       添加雷达扫描线
       viewer
       cartographicCenter 扫描中心
       radius  半径 米
       scanColor 扫描颜色
       duration 持续时间 毫秒
       */
      getScanSegmentShader() {
        var scanSegmentShader = "\n\
                    uniform sampler2D colorTexture;\n\
                    uniform sampler2D depthTexture;\n\
                    varying vec2 v_textureCoordinates;\n\
                    uniform vec4 u_scanCenterEC;\n\
                    uniform vec3 u_scanPlaneNormalEC;\n\
                    uniform float u_radius;\n\
                    uniform vec4 u_scanColor;\n\
                    \n\
                    vec4 toEye(in vec2 uv,in float depth)\n\
                    {\n\
                                vec2 xy = vec2((uv.x * 2.0 - 1.0),(uv.y * 2.0 - 1.0));\n\
                                vec4 posIncamera = czm_inverseProjection * vec4(xy,depth,1.0);\n\
                                posIncamera = posIncamera/posIncamera.w;\n\
                                return posIncamera;\n\
                    }\n\
                    \n\
                    vec3 pointProjectOnPlane(in vec3 planeNormal,in vec3 planeOrigin,in vec3 point)\n\
                    {\n\
                                vec3 v01 = point - planeOrigin;\n\
                                float d = dot(planeNormal,v01);\n\
                                return (point-planeNormal * d);\n\
                    }\n\
                    float getDepth(in vec4 depth)\n\
                    {\n\
                                float z_window = czm_unpackDepth(depth);\n\
                                z_window = czm_reverseLogDepth(z_window);\n\
                                float n_range = czm_depthRange.near;\n\
                                float f_range = czm_depthRange.far;\n\
                                return (2.0 * z_window - n_range - f_range)/(f_range-n_range);\n\
                    } \n\
                    void main()\n\
                    {\n\
                                gl_FragColor = texture2D(colorTexture,v_textureCoordinates);\n\
                                float depth = getDepth(texture2D(depthTexture,v_textureCoordinates));\n\
                                vec4 viewPos = toEye(v_textureCoordinates,depth);\n\
                                vec3 prjOnPlane = pointProjectOnPlane(u_scanPlaneNormalEC.xyz,u_scanCenterEC.xyz,viewPos.xyz);\n\
                                float dis = length(prjOnPlane.xyz - u_scanCenterEC.xyz);\n\
                                if(dis<u_radius)\n\
                                {\n\
                                    float f = 1.0-abs(u_radius - dis )/ u_radius;\n\
                                    f = pow(f,4.0);\n\
                                    gl_FragColor = mix(gl_FragColor,u_scanColor,f);\n\
                                }\n\
                    } \n\ ";
        return scanSegmentShader;
      },
      //添加圆形区域闪烁
      flashCircle() {
        var x = 1;
        var flog = true;
        let _this = this
        _this.viewer.entities.add({
          name: "圆形区域闪烁",
          position: Cesium.Cartesian3.fromDegrees(114.292832, 30.584519, 0),
          ellipse: {
            semiMinorAxis: 2000.0,//圆的大小
            semiMajorAxis: 2000.0,
            height: 0,
            material: new Cesium.ColorMaterialProperty(new Cesium.CallbackProperty(function () {
              if (flog) {
                x = x - 0.05;
                if (x <= 0) {
                  flog = false;
                }
              } else {
                x = x + 0.05;
                if (x >= 1) {
                  flog = true;
                }
              }
              return Cesium.Color.RED.withAlpha(x);//通过循环改变材质实现闪烁效果
            }, false))
          }
        });
      },
//        闪圆,问题在于如何关闭
      flashRound() {
        var x = 1;
        var flog = true;
        let _this = this
        _this.viewer.entities.add({
          name: "圆点闪烁",
          position: Cesium.Cartesian3.fromDegrees(114.292832 + 0.03, 30.584519 + 0.03, 0),//圆点闪烁的位置
          point: {
            show: true, // default
            color: new Cesium.CallbackProperty(function () {
              if (flog) {
                x = x - 0.05;
                if (x <= 0) {
                  flog = false;
                }
              } else {
                x = x + 0.05;
                if (x >= 1) {
                  flog = true;
                }
              }
              return Cesium.Color.RED.withAlpha(x);//通过循环改变透明度实现闪烁效果
            }, false),
            pixelSize: 20, // 闪圆的大小
            outlineWidth: 0
          }
        });
      },
      //画面，画点等函数
      draw_picture(index) {
        this.draw_able = true
        var me = this
        if (index === 1) {//画点
          this.index = 1
        } else if (index === 2) {//画线
          this.draw_able = true
          this.line_able = true
          this.index = 2
        } else if (index === 3) {//画面
          this.draw_able = true
          this.polygon_able = true
          this.index = 3
        } else if (index === 4) {//画矩形
          this.draw_able = true
          this.rectangle_able = true
          this.index = 4
        } else if (index === 5) {//测距
          this.draw_able = true
          this.getDistance_able = true
          this.index = 5
        } else if (index === 6) {//测面
          this.draw_able = true
          this.getArea_able = true
          this.index = 6
        }
        this.handler.setInputAction(function (e) {
          if (me.polygon_able || me.getArea_able || me.rectangle_able) {//画面 测面右键
            me.terminateShape();
            me.polygon_able = false
            me.getArea_able = false
            me.rectangle_able = false
          } else if (me.getDistance_able) {
            me.polylineLastPoint = me.activeShapePoints[me.activeShapePoints.length - 1];//得到最后一个点
            me.viewer.entities.remove(me.polylinePoint);//移除最后一个节点，换成终点
            me.polylinePoint = me.viewer.entities.add({
              position: me.polylineLastPoint,
              label: {
                text: '终点',
                font: '20px Helvetica',
                fillColor: Cesium.Color.WHITE,
                eyeOffset: new Cesium.Cartesian3(0, 0, -150)
              }
            });
            me.getDistance_able = false
          }
          me.line_able = false
          me.lastPosition = null//清空上一个点
          me.linePositionData = []//清空线上的点
          me.polylinePoint = []//清空
          me.draw_able = false
          me.activeShapePoints = []
          me.count = 1//初始化
        }, Cesium.ScreenSpaceEventType.RIGHT_CLICK);//右键结束绘图
      },

      terminateShape() {//绘制最终图形
        var me = this;
        if (me.activeShapePoints.length) {
          if (me.polygon_able || me.rectangle_able || me.getArea_able) {
            if (me.polygon_able) {
              me.createPolygon(me.activeShapePoints);//绘制最终面
              me.text = '新建画面'
            } else if (me.rectangle_able) {
              me.text = '新建矩形'
            } else if (me.getArea_able) {
              me.createPolygon(me.activeShapePoints);//绘制最终面
              var area = ((me.getArea(me.activeShapePoints)) * 1000000).toFixed(4) + '平方米';//原面积的单位为平方公里
              me.text = area;
            }
            me.polygonCenter = Cesium.BoundingSphere.fromPoints(me.activeShapePoints).center;//所有的点画完后，得到多边形中心
            me.polygonCenter = Cesium.Ellipsoid.WGS84.scaleToGeodeticSurface(me.polygonCenter);
            me.viewer.entities.add({
              position: me.polygonCenter,
              label: {
                text: me.text,
                font: '20px Helvetica',
                fillColor: Cesium.Color.WHITE,
                eyeOffset: new Cesium.Cartesian3(0, 0, -150)
              }
            });
          }
        }
        me.viewer.entities.remove(me.floatingPoint); //去除动态点图形（当前鼠标点）
        me.viewer.entities.remove(me.polygon); //去除动态图形
        me.floatingPoint = undefined;
        me.activeShape = undefined;
        me.activeShapePoints = [];
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
        //第一条航线
//        var flightData= [{"longitude":114.54207,"latitude":30.67206,"height":-1},{"longitude":114.54202,"latitude":30.66802,"height":-1},{"longitude":114.54896,"latitude":30.65405,"height":-1},{"longitude":114.56185,"latitude":30.63212,"height":-2},{"longitude":114.56756,"latitude":30.61987,"height":-1},{"longitude":114.57712,"latitude":30.60163,"height":-1},{"longitude":114.59272,"latitude":30.57847,"height":-1},{"longitude":114.62799,"latitude":30.55966,"height":-1},{"longitude":114.64263,"latitude":30.56722,"height":-1},{"longitude":114.67968,"latitude":30.57833,"height":-1},{"longitude":114.70862,"latitude":30.58902,"height":-1},{"longitude":114.76289,"latitude":30.61804,"height":-1},{"longitude":114.79516,"latitude":30.61570,"height":-1},{"longitude":114.83342,"latitude":30.59835,"height":-1},{"longitude":114.84145,"latitude":30.57843,"height":-1},{"longitude":114.83960,"latitude":30.56437,"height":-1},{"longitude":114.83683,"latitude":30.53635,"height":-1},{"longitude":114.83397,"latitude":30.50823,"height":-1},{"longitude":114.83476,"latitude":30.48289,"height":-1},{"longitude":114.84023,"latitude":30.45833,"height":-1},{"longitude":114.85853,"latitude":30.43707,"height":-1},{"longitude":114.88539,"latitude":30.42023,"height":-1},{"longitude":114.89741,"latitude":30.41690,"height":-1},{"longitude":114.91089,"latitude":30.41498,"height":-1},{"longitude":114.94166,"latitude":30.41261,"height":-1},{"longitude":114.96872,"latitude":30.41106,"height":-1},{"longitude":115.01245,"latitude":30.41153,"height":-1},{"longitude":115.04500,"latitude":30.40619,"height":-1},{"longitude":115.06555,"latitude":30.39794,"height":-1},{"longitude":115.08789,"latitude":30.38173,"height":-1},{"longitude":115.10873,"latitude":30.35088,"height":-1},{"longitude":115.10847,"latitude":30.32160,"height":-1},{"longitude":115.08760,"latitude":30.28934,"height":-1},{"longitude":115.07826,"latitude":30.27200,"height":-1},{"longitude":115.07506,"latitude":30.26156,"height":-1},{"longitude":115.07691,"latitude":30.24325,"height":-1},{"longitude":115.09364,"latitude":30.22377,"height":-1},{"longitude":115.11237,"latitude":30.21495,"height":-1},{"longitude":115.15076,"latitude":30.21245,"height":-1},{"longitude":115.18405,"latitude":30.22289,"height":-1},{"longitude":115.21490,"latitude":30.21017,"height":-1},{"longitude":115.23034,"latitude":30.19283,"height":-1},{"longitude":115.24370,"latitude":30.18129,"height":-1},{"longitude":115.26195,"latitude":30.16000,"height":-1},{"longitude":115.27321,"latitude":30.14648,"height":-1}]
////        第二条航线的经纬度
        var flightData = [{"longitude": 115.26390, "latitude": 30.15192, "height": -1}, {
          "longitude": 115.25123,
          "latitude": 30.16539,
          "height": -1
        }, {"longitude": 115.23922, "latitude": 30.17797, "height": -1}, {
          "longitude": 115.23035,
          "latitude": 30.18608,
          "height": -1
        }, {"longitude": 115.21618, "latitude": 30.20479, "height": -1}, {
          "longitude": 115.19935,
          "latitude": 30.21476,
          "height": -1
        }, {"longitude": 115.17668, "latitude": 30.21768, "height": -1}, {
          "longitude": 115.15612,
          "latitude": 30.21459,
          "height": -1
        }, {"longitude": 115.14390, "latitude": 30.20889, "height": -1}, {
          "longitude": 115.12566,
          "latitude": 30.20927,
          "height": -1
        }, {"longitude": 115.10630, "latitude": 30.21259, "height": -1}, {
          "longitude": 115.08923,
          "latitude": 30.22101,
          "height": -1
        }, {"longitude": 115.07676, "latitude": 30.23179, "height": -1}, {
          "longitude": 115.07114,
          "latitude": 30.24040,
          "height": -1
        }, {"longitude": 115.06793, "latitude": 30.25458, "height": -1}, {
          "longitude": 115.07298,
          "latitude": 30.27014,
          "height": -1
        }, {"longitude": 115.07917, "latitude": 30.28469, "height": -1}, {
          "longitude": 115.08471,
          "latitude": 30.29643,
          "height": -1
        }, {"longitude": 115.08498, "latitude": 30.31843, "height": -1}, {
          "longitude": 115.08316,
          "latitude": 30.33080,
          "height": -1
        }, {"longitude": 115.07613, "latitude": 30.35094, "height": -1}, {
          "longitude": 115.05811,
          "latitude": 30.37917,
          "height": -1
        }, {"longitude": 115.03532, "latitude": 30.39796, "height": -1}, {
          "longitude": 115.00940,
          "latitude": 30.40539,
          "height": -1
        }, {"longitude": 114.98450, "latitude": 30.40351, "height": -1}, {
          "longitude": 114.94858,
          "latitude": 30.40313,
          "height": -1
        }, {"longitude": 114.92275, "latitude": 30.40954, "height": -1}, {
          "longitude": 114.89235,
          "latitude": 30.41269,
          "height": -1
        }, {"longitude": 114.85739, "latitude": 30.42360, "height": -1}, {
          "longitude": 114.84164,
          "latitude": 30.43038,
          "height": -1
        }, {"longitude": 114.82849, "latitude": 30.44543, "height": -1}, {
          "longitude": 114.82502,
          "latitude": 30.46364,
          "height": -1
        }, {"longitude": 114.82501, "latitude": 30.48692, "height": -1}, {
          "longitude": 114.82549,
          "latitude": 30.49848,
          "height": -1
        }, {"longitude": 114.82782, "latitude": 30.51665, "height": -1}, {
          "longitude": 114.83015,
          "latitude": 30.53301,
          "height": -1
        }, {"longitude": 114.83233, "latitude": 30.55918, "height": -1}, {
          "longitude": 114.83406,
          "latitude": 30.57235,
          "height": -1
        }, {"longitude": 114.82183, "latitude": 30.59913, "height": -1}, {
          "longitude": 114.80554,
          "latitude": 30.60878,
          "height": -1
        }, {"longitude": 114.77815, "latitude": 30.61422, "height": -1}, {
          "longitude": 114.75564,
          "latitude": 30.60966,
          "height": -1
        }, {"longitude": 114.74401, "latitude": 30.59999, "height": -1}, {
          "longitude": 114.73082,
          "latitude": 30.58931,
          "height": -1
        }, {"longitude": 114.70874, "latitude": 30.57887, "height": -1}, {
          "longitude": 114.67608,
          "latitude": 30.57246,
          "height": -1
        }, {"longitude": 114.65197, "latitude": 30.56909, "height": -1}, {
          "longitude": 114.62552,
          "latitude": 30.55452,
          "height": -1
        }, {"longitude": 114.60471, "latitude": 30.55901, "height": -1}, {
          "longitude": 114.58576,
          "latitude": 30.57246,
          "height": -1
        }, {"longitude": 114.57345, "latitude": 30.59102, "height": -1}, {
          "longitude": 114.56203,
          "latitude": 30.61703,
          "height": -1
        }, {"longitude": 114.55570, "latitude": 30.63393, "height": -1}, {
          "longitude": 114.54903,
          "latitude": 30.64397,
          "height": -1
        }, {"longitude": 114.54207, "latitude": 30.67206, "height": -1}]

//点的个数较密集的第二条航道
//        var flightData = [{"longitude":115.26975,"latitude":30.14760,"height":-1},
//          {"longitude":115.26658,"latitude":30.15185,"height":-1},
//          {"longitude":115.26195,"latitude":30.15644,"height":-1},
//          {"longitude":115.25646,"latitude":30.16228,"height":-1},
//          {"longitude":115.25213,"latitude":30.16721,"height":-1},
//          {"longitude":115.24751,"latitude":30.17276,"height":-1},
//          {"longitude":115.24220,"latitude":30.17748,"height":-1},
//          {"longitude":115.23755,"latitude":30.17989,"height":-1},
//          {"longitude":115.23297,"latitude":30.18379,"height":-1},
//          {"longitude":115.22859,"latitude":30.18804,"height":-1},
//          {"longitude":115.22558,"latitude":30.19693,"height":-1},
//          {"longitude":115.22056,"latitude":30.20161,"height":-1},
//          {"longitude":115.21515,"latitude":30.20840,"height":-1},
//          {"longitude":115.20789,"latitude":30.21240,"height":-1},
//          {"longitude":115.20116,"latitude":30.21671,"height":-1},
//          {"longitude":115.18971,"latitude":30.22062,"height":-1},
//          {"longitude":115.17726,"latitude":30.21912,"height":-1},
//          {"longitude":115.16374,"latitude":30.21705,"height":-1},
//          {"longitude":115.15962,"latitude":30.21855,"height":-1},
//          {"longitude":115.15367,"latitude":30.21507,"height":-1},
//          {"longitude":115.15032,"latitude":30.21187,"height":-1},
//          {"longitude":115.14171,"latitude":30.21082,"height":-1},
//          {"longitude":115.12911,"latitude":30.21186,"height":-1},
//          {"longitude":115.12364,"latitude":30.21196,"height":-1},
//          {"longitude":115.10882,"latitude":30.21421,"height":-1},
//          {"longitude":115.09719,"latitude":30.21750,"height":-1},
//          {"longitude":115.08797,"latitude":30.22425,"height":-1},
//          {"longitude":115.07688,"latitude":30.23393,"height":-1},
//          {"longitude":115.07139,"latitude":30.24408,"height":-1},
//          {"longitude":115.07102,"latitude":30.25518,"height":-1},
//          {"longitude":115.07333,"latitude":30.26587,"height":-1},
//          {"longitude":115.07761,"latitude":30.27891,"height":-1},
//          {"longitude":115.07875,"latitude":30.29568,"height":-1},
//          {"longitude":115.07850,"latitude":30.31178,"height":-1},
//          {"longitude":115.07975,"latitude":30.32844,"height":-1},
//          {"longitude":115.07712,"latitude":30.34304,"height":-1},
//          {"longitude":115.07019,"latitude":30.35782,"height":-1},
//          {"longitude":115.06356,"latitude":30.36863,"height":-1},
//          {"longitude":115.05421,"latitude":30.38260,"height":-1},
//          {"longitude":115.03986,"latitude":30.39367,"height":-1},
//          {"longitude":115.02362,"latitude":30.40179,"height":-1},
//          {"longitude":115.00901,"latitude":30.40360,"height":-1},
//          {"longitude":114.99281,"latitude":30.40201,"height":-1},
//          {"longitude":114.97667,"latitude":30.40240,"height":-1},
//          {"longitude":114.95702,"latitude":30.40236,"height":-1},
//          {"longitude":114.94627,"latitude":30.40368,"height":-1},
//          {"longitude":114.93114,"latitude":30.40770,"height":-1},
//          {"longitude":114.91566,"latitude":30.40999,"height":-1},
//          {"longitude":114.89645,"latitude":30.41193,"height":-1},
//          {"longitude":114.88024,"latitude":30.41519,"height":-1},
//          {"longitude":114.86765,"latitude":30.42093,"height":-1},
//          {"longitude":114.85384,"latitude":30.42425,"height":-1},
//          {"longitude":114.83640,"latitude":30.43211,"height":-1},
//          {"longitude":114.83068,"latitude":30.43594,"height":-1},
//          {"longitude":114.82724,"latitude":30.44198,"height":-1},
//          {"longitude":114.82562,"latitude":30.44521,"height":-1},
//          {"longitude":114.82484,"latitude":30.44936,"height":-1},
//          {"longitude":114.82389,"latitude":30.45564,"height":-1},
//          {"longitude":114.82406,"latitude":30.45992,"height":-1},
//          {"longitude":114.82372,"latitude":30.47406,"height":-1},
//          {"longitude":114.82516,"latitude":30.49165,"height":-1},
//          {"longitude":114.82694,"latitude":30.50335,"height":-1},
//          {"longitude":114.82906,"latitude":30.51491,"height":-1},
//          {"longitude":114.83101,"latitude":30.52831,"height":-1},
//          {"longitude":114.83284,"latitude":30.54196,"height":-1},
//          {"longitude":114.83305,"latitude":30.55881,"height":-1},
//          {"longitude":114.83321,"latitude":30.57829,"height":-1},
//          {"longitude":114.82619,"latitude":30.59483,"height":-1},
//          {"longitude":114.81247,"latitude":30.60426,"height":-1},
//          {"longitude":114.80255,"latitude":30.60998,"height":-1},
//          {"longitude":114.79638,"latitude":30.61162,"height":-1},
//          {"longitude":114.79082,"latitude":30.61401,"height":-1},
//          {"longitude":114.78054,"latitude":30.61543,"height":-1},
//          {"longitude":114.77067,"latitude":30.61614,"height":-1},
//          {"longitude":114.75874,"latitude":30.61249,"height":-1},
//          {"longitude":114.74158,"latitude":30.60359,"height":-1},
//          {"longitude":114.72967,"latitude":30.59167,"height":-1},
//          {"longitude":114.70995,"latitude":30.58064,"height":-1},
//          {"longitude":114.68611,"latitude":30.57672,"height":-1},
//          {"longitude":114.66146,"latitude":30.57272,"height":-1},
//          {"longitude":114.63528,"latitude":30.56356,"height":-1},
//          {"longitude":114.62677,"latitude":30.55645,"height":-1},
//          {"longitude":114.61444,"latitude":30.55796,"height":-1},
//          {"longitude":114.60458,"latitude":30.56169,"height":-1},
//          {"longitude":114.58576,"latitude":30.57697,"height":-1},
//          {"longitude":114.57156,"latitude":30.59981,"height":-1},
//          {"longitude":114.56362,"latitude":30.62035,"height":-1},
//          {"longitude":114.55112,"latitude":30.64312,"height":-1},
//          {"longitude":114.54914,"latitude":30.65246,"height":-1}
//      ];
        for (let i = 0; i < flightData.length; i++) {
          const dataPoint = flightData[i];
          const position = Cesium.Cartesian3.fromDegrees(dataPoint.longitude, dataPoint.latitude, dataPoint.height);//将地理坐标转换为天地图坐标
          this.viewer.entities.add({
            description: `Location: (${dataPoint.longitude}, ${dataPoint.latitude}, ${dataPoint.height})`,
            position: position,
            point: {pixelSize: 10, color: Cesium.Color.RED}
          });
        }

        let me = this;
        new Cesium.ScreenSpaceEventHandler(this.viewer.canvas).setInputAction(function (e) {
          var ellipsoid = me.viewer.scene.globe.ellipsoid
          var cartesian = me.viewer.camera.pickEllipsoid(e.endPosition, ellipsoid)
          var cartographic = me.viewer.scene.globe.ellipsoid.cartesianToCartographic(cartesian)
          me.mousePosition.height = Math.ceil(me.viewer.camera.positionCartographic.height)
          me.mousePosition.lat = Cesium.Math.toDegrees(cartographic.latitude)
          me.mousePosition.lng = Cesium.Math.toDegrees(cartographic.longitude)//获得鼠标所在位置
          if (me.polygon_able || me.getArea_able) {//画面时获取动态点
            if (Cesium.defined(me.floatingPoint)) {
              var newPosition = me.viewer.scene.pickPosition(e.endPosition);//获取鼠标点
              console.log(newPosition)//未输出
              if (Cesium.defined(newPosition)) {
                me.floatingPoint.position.setValue(newPosition);
                me.activeShapePoints.pop();//去除动态点
                me.activeShapePoints.push(newPosition);//将最后一个点push进动态点集合
              }
            }
          }
        }, Cesium.ScreenSpaceEventType.MOUSE_MOVE);

        this.handler.setInputAction(function (e) { //单击开始绘制
          if (me.draw_able) {
            if (me.index === 1) {//点单击
              var text = '新建标点';
              me.createPoint2(e, text)//绘制点
            } else if (me.index === 2 || me.index === 5) {//线，测距单击
              var earthPosition = me.viewer.scene.camera.pickEllipsoid(e.position, me.viewer.scene.globe.ellipsoid);
              if (Cesium.defined(earthPosition)) {
                if (me.activeShapePoints.length === 0) {
                  if (me.index === 2) {//画线创建编号
                    var text = me.count.toString()
                    me.createPoint2(e, text);
                  } else {//测距添加起点
                    var text = '起点';
                    me.createPoint2(e, text);
                  }
                }
                me.activeShapePoints.push(earthPosition);//将得到的点数据存入活动点集中
                if (me.line_able || me.getDistance_able) {
                  if (me.lastPosition != null) {//画线时得到两点的中心
                    me.linePositionData = [] //清空线数据，存入新的数据
                    me.linePositionData.push(me.lastPosition)
                    me.linePositionData.push(earthPosition)
                    me.polylineCenter = Cesium.BoundingSphere.fromPoints(me.linePositionData).center;//多边形中心
                    me.polylineCenter = Cesium.Ellipsoid.WGS84.scaleToGeodeticSurface(me.polylineCenter);
                    me.polyline = me.createPolyline()//两点成线
                    if (me.line_able) {
                      var point = me.createPoint(e);//添加线上的点
                      me.text = '新建画线';//画线时在线的中间添加新建画线
                      me.count++;//点的个数自增
                      me.viewer.entities.add({//添加点的标号，从2开始
                        position: earthPosition,
                        label: {
                          text: me.count.toString(),
                          font: '20px Helvetica',
                          fillColor: Cesium.Color.WHITE,
                          eyeOffset: new Cesium.Cartesian3(0, 0, -150)
                        }
                      });
                    } else if (me.getDistance_able) {
                      var point = me.createPoint(e);//添加线上的点
                      if (me.activeShapePoints.length > 1) {//消除undefined bug
                        me.text = me.line_text//得到距离
                      }
                      me.polylinePoint = me.viewer.entities.add({//显示节点
                        position: earthPosition,
                        label: {
                          text: '节点',
                          font: '20px Helvetica',
                          fillColor: Cesium.Color.WHITE,
                          eyeOffset: new Cesium.Cartesian3(0, 0, -150)
                        }
                      });
                    }
                    me.viewer.entities.add({//显示新建画线或者距离
                      position: me.polylineCenter,
                      label: {
                        text: me.text,
                        font: '20px Helvetica',
                        fillColor: Cesium.Color.WHITE,
                        eyeOffset: new Cesium.Cartesian3(0, 0, -150)
                      }
                    });
                  }
                  me.lastPosition = earthPosition//得到新的点
                }
                me.activeShapePoints.push(earthPosition);
              }
            } else if (me.index === 3 || me.index === 4 || me.index === 6) {//面单击,矩形,测面单击
              var earthPosition = me.viewer.scene.camera.pickEllipsoid(e.position, me.viewer.scene.globe.ellipsoid);
              if (Cesium.defined(earthPosition)) {
                var point = me.createPoint(e);//产生点
                me.viewer.entities.add({//添加点的标号
                  position: earthPosition,
                  label: {
                    text: me.count.toString(),
                    font: '20px Helvetica',
                    fillColor: Cesium.Color.WHITE,
                    eyeOffset: new Cesium.Cartesian3(0, 0, -150)
                  }
                });
                me.count++;
                if (me.activeShapePoints.length === 0) {//第一个点
                  me.floatingPoint = point;
                  me.activeShapePoints.push(earthPosition);//活动点的集合
                  var dynamicPositions = new Cesium.CallbackProperty(function () {//得到用于绘制面的点
                    if (me.index === 3 || me.index === 6) {
                      return new Cesium.PolygonHierarchy(me.activeShapePoints);
                    }
                  }, false);
                  me.polygon = me.createPolygon(dynamicPositions);//绘制面
                  if (me.rectangle_able) {//绘制矩形
                    me.rectangle = me.createRectangle();
                  }
                }
                me.activeShapePoints.push(earthPosition);
              }
            }
          }
        }, Cesium.ScreenSpaceEventType.LEFT_CLICK);
      },
      //画点
      createPoint(e) {//左键单击产生点
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
        var drawpolyline = $this.viewer.entities.add({
          polyline: {
            positions: $this.activeShapePoints,
            material: Cesium.Color.RED,
            width: 3,
            clampToGround: true
          }
        });
        if ($this.index === 5) {
          $this.line_text = $this.getSpaceDistance($this.activeShapePoints);//如果测距得到两点距离
        }
      },

      //创建面
      createPolygon(positionsData) {
        var $this = this;
        var polygon = $this.viewer.entities.add({
          polygon: {
            hierarchy: positionsData,
            material: new Cesium.ColorMaterialProperty(Cesium.Color.BLUE.withAlpha(0.8))
          }
        });
      },

      //  矩形
      createRectangle() {
        var $this = this;
        var arr = typeof $this.activeShapePoints.getValue === 'function' ? $this.activeShapePoints.getValue(0) : $this.activeShapePoints;
        var rectangle = $this.viewer.entities.add({
          rectangle: {
            coordinates: new Cesium.CallbackProperty(function () {
              var obj = Cesium.Rectangle.fromCartesianArray(arr);
//              if(obj.west==obj.east){ obj.east+=0.000001};//偏移修正
//              if(obj.south==obj.north){obj.north+=0.000001};//偏移修正
              return obj;
            }, false),
            material: Cesium.Color.RED.withAlpha(0.5)
          }
        });
      },

      //  测距
      //同时产生点和编号
      createPoint2(e, text) {
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
            style: Cesium.LabelStyle.FILL,
            outlineWidth: 1,
            fillColor: Cesium.Color.WHITE,
            showBackground: false,
            backgroundColor: Cesium.Color.ORANGE.withAlpha(0.6),
            horizontalOrigin: Cesium.HorizontalOrigin.LEFT,
            pixelOffset: new Cesium.Cartesian2(5.0, -20.0),
          }
        });
      },
      //测距函数
      getSpaceDistance(positions) {
        for (var i = 0; i < positions.length - 1; i++) {
          var point1cartographic = Cesium.Cartographic.fromCartesian(positions[i]);
          var point2cartographic = Cesium.Cartographic.fromCartesian(positions[i + 1]);
          /**根据经纬度计算出距离**/
          var geodesic = new Cesium.EllipsoidGeodesic();
          geodesic.setEndPoints(point1cartographic, point2cartographic);
          var s = geodesic.surfaceDistance;
          //返回两点之间的距离
          s = Math.sqrt(Math.pow(s, 2) + Math.pow(point2cartographic.height - point1cartographic.height, 2)).toFixed(4);
        }
        return s + 'm'
      },

//    新的测面公式
      getArea(points) {
        var res = 0;
        var _this = this
        //拆分三角曲面
        for (var i = 0; i < points.length - 2; i++) {
          var j = (i + 1) % points.length;
          var k = (i + 2) % points.length;
          var totalAngle = _this.Angle(points[i], points[j], points[k]);
          var dis_temp1 = _this.getDistance(points[i], points[j]);
          var dis_temp2 = _this.getDistance(points[j], points[k]);
          res += dis_temp1 * dis_temp2 * Math.abs(Math.sin(totalAngle));
        }
        return (res / 1000000.0).toFixed(8);
      },

      /*角度*/
      Angle(p1, p2, p3) {
        var _this = this
        var bearing21 = _this.Bearing(p2, p1);
        var bearing23 = _this.Bearing(p2, p3);
        var angle = bearing21 - bearing23;
        if (angle < 0) {
          angle += 360;
        }
        return angle;
      },

      /*方向*/ //计算方法不同
      Bearing(from, to) {
        var _this = this
        var cartographic_from = Cesium.Cartographic.fromCartesian(from);
        var cartographic_to = Cesium.Cartographic.fromCartesian(to);
        var lon_from = Cesium.Math.toDegrees(cartographic_from.longitude);
        var lat_from = Cesium.Math.toDegrees(cartographic_from.latitude);

        var lon_to = Cesium.Math.toDegrees(cartographic_to.longitude);
        var lat_to = Cesium.Math.toDegrees(cartographic_to.latitude);

        var lat1 = lat_from * _this.radiansPerDegree;
        var lon1 = lon_from * _this.radiansPerDegree;
        var lat2 = lat_to * _this.radiansPerDegree;
        var lon2 = lon_to * _this.radiansPerDegree;
        var angle = -Math.atan2(Math.sin(lon1 - lon2) * Math.cos(lat2), Math.cos(lat1) * Math.sin(lat2) - Math.sin(lat1) * Math.cos(lat2) * Math.cos(lon1 - lon2));
        if (angle < 0) {
          angle += Math.PI * 2.0;
        }
        angle = angle * _this.degreesPerRadian;//角度
        return angle;
      },

      getDistance(point1, point2) {
        var point1cartographic = Cesium.Cartographic.fromCartesian(point1);
        var point2cartographic = Cesium.Cartographic.fromCartesian(point2);
        /**根据经纬度计算出距离**/
        var geodesic = new Cesium.EllipsoidGeodesic();
        geodesic.setEndPoints(point1cartographic, point2cartographic);
        var s = geodesic.surfaceDistance;
        //返回两点之间的距离
        s = Math.sqrt(Math.pow(s, 2) + Math.pow(point2cartographic.height - point1cartographic.height, 2));
        return s;
      },
      //  清除
      clearDrawingBoard() {
        this.viewer.entities.removeAll();//删除全部
      },
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

  .html-box{
    height: 20px;
    width:30px;
    border: solid 1px #00ff00;
  }

</style>
