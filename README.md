# Wap 自适应开发 
## 设置html fontSize (以下“750”为设计稿宽度)
```html
<script>
    !function(n,e){var t=e.documentElement,i='orientationchange'in n?'orientationchange':'resize',d=function(){var n=t.clientWidth
        n&&(t.style.fontSize=100*(n/750)+'px')}
        e.addEventListener&&(n.addEventListener(i,d,!1),e.addEventListener('DOMContentLoaded',d,!1),d())}(window,document)
</script>
```

## SASS 代码
```sass
/**
 * 引用重置样式
 */
@import '../reset';
/**
 * [$fontSizeBase 字体基数]
 * @type {[type]}
 */
$fontSizeBase: 100px;
/**
 * [$version 版本号]
 * @type {String}
 */
$version: '?v=201608261701';
/**
 * [$url 背景图片目录路径]
 * @type {String}
 */
$url: '../../images/schedule/';
/**
 * [px2rem px单位转rem单位]
 * @param  {[type]} $px [参数px值]
 * @return {[type]}     [返回rem单位]
 */
@function px2rem($px){
	@if(type-of($px) == 'number'){
		@return $px / $fontSizeBase * 1rem;		
	}
}
/**
 * [sprite 雪碧图]
 * @param  {[type]} $bgW [合成图宽度]
 * @param  {[type]} $bgH [合成图高度]
 * @param  {[type]} $w   [单个图宽度]
 * @param  {[type]} $h   [单个图高度]
 * @param  {[type]} $x   [单个图x轴位移]
 * @param  {[type]} $y   [单个图y轴位移]
 */
@mixin sprite($bgW, $bgH, $w, $h, $x, $y){ 
	@function spritePosX($bgW, $x, $w){
		@if ($bgW / 1px - $w / 1px == 0) {
			@return 0;
		} @else {
			@return $x / ($bgW - $w) * 100%;
		}	
	}
	@function spritePosY($bgH, $y, $h){
		@if ($bgH / 1px - $h / 1px == 0) {
			@return 0;
		} @else {
			@return $y / ($bgH - $h) * 100%;
		}	
	}
	@function spriteSize($bgW, $w){
		@return $bgW / $w * 100%;
	}
	background-position: spritePosX($bgW, $x, $w) spritePosY($bgH, $y, $h); background-size: spriteSize($bgW, $w); width: px2rem($w); height: px2rem($h);
}
/**
 * [text-middle 文字垂直居中]
 * @param  {[type]} $h [高度]
 */
@mixin text-middle($h) { height: px2rem($h); line-height: px2rem($h);}
/**
 * [left 左浮动]
 */
.left{ float: left; display: inline;}
/**
 * [right 右浮动]
 */
.right{ float: right; display: inline;}
/**
 * [clearfix 清浮动]
 */
.clearfix{
    &:before, &:after{ display: table; content: ""; line-height: 0;}
    &:after{ clear: both;}
}
/**
 * [overflow 超过宽度加省略号]
 */
.text-overflow{ overflow: hidden; text-overflow: ellipsis; white-space: nowrap;}
/**
 * [indent 背景图片添加文字描述]
 */
.text-seo{ text-indent: -999999rem;}
```
