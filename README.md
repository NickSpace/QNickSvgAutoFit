# QNickSvgAutoFit

QNickSvgAutoFit是地图控制插件
主要功能是缩放地图大小，点击省份自动对焦功能的小插件。

QNickSvgAutoFit is map controller, it can be scale map and auto fit click area.

## How it works

- It work base on [Snap.svg](http://snapsvg.io/) 
- Import SVG path and map data.

## Usage

- Include jQuery , Snap.svg, QNickSvgAutoFit.
- Import MapData.
- Call QNickSvgAutoFit.

``` html
<script src="./js/snap.svg-min.js"></script>
<script src="./js/jquery-2.1.1.min.js"></script>
<script src="./js/jquery.svg_autofit.1.0.1.js"></script>
<script src="./js/chinaMapData.js"></script>
<script>
$(document).ready(function(){
	var mapCtrl = $('#svg').QNickSvgAutoFit({
		mapData:chinaMapConfig
		,onClick:function(e){
			console.log('你选择了：'+$(e).find('text').text());
		}
		,onLoad:function(e){
			e.autoFit();
		}
	});
  });
</script>
```


## Options


``` javascript
defaults = {	// defaults option
    maxScale: 3		//max scale on auto fit 
    ,minScale: 0.6	//min scale on auto fit 
    ,mapData : {}	//SVG and other map data
    ,shapesColor:'#FF4239'		
    ,strokeColor:'#fff'			
    ,shapesColorOn:'#FF4239'
    ,strokeColorOn:'#fff'
    ,FontColorOn:'#fff'
    ,lightFontColor:'#fff'		//defualt font color
    ,darkFontColor:'#6f3838'	//under 30% font color
    ,scaleDuration:500		//animation duration
    ,debugMode:false		//debug mode 
    ,selectClassName:'sheng'
    ,selectShapeClassName:'shengShape'
    ,selectTextClassName:'shengText'
    ,scalePadding:30		//padding for auto scale
    ,fitPadding:10			//padding for auto fit[total map scale]
}

status = {		//init map position
    'mapScale' : 1      //放大比例
    ,'centerX' : 'center'    //缩放中心点x坐标
    ,'centerY' : 'center'    //缩放中心点y坐标
    ,'moveX' : 'center'    //横向移动x坐标
    ,'moveY' : 'center'    //纵向移动y坐标
}
```
## Methods

- `scaleMap(scaleVal)`: `scaleVal:Number` 缩放比例.
- `autoScale('shengName')`: `shengName:string` 选择省.
- `autoFit()`: 自动对焦整个地图.
- `customScale(scaleVal,center,position)`: 自定义对焦区域.

## Events

- `onClick`: 当选择省份的时候触发onClick方法.
- `onLoad`: 当初始化完成后触发.

To subscribe to events use **Type1**:

```html
<script>
var mapCtrl = $('#svg').QNickSvgAutoFit({
	mapData:chinaMapConfig
     	,onClick:function(e){
     		console.log('你选择了：'+$(e).find('text').text());
	},onLoad:function(e){
		e.autoFit();
	}
});
</script>
```

To subscribe to events use **Type2**:

```html
<script>
// onLoad Event Must come before init.
// 定义onLoad事件顺序很重要~.
$('#svg').on('onLoad',function(e,mapCtrl){
     mapCtrl.autoScale('zhejiang');
});

//at the onLoad event method after.
var mapCtrl = $('#svg').QNickSvgAutoFit({
	mapData:chinaMapConfig
});

mapCtrl.on('onClick',function(e,target){
	console.log('你选择了：'+$(target).find('text').text());
});
</script>
```

