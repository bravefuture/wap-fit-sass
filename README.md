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
@import '../reset';

$fontSizeBase: 100px;
$version: '?v=201607271515';
$url: '../images/index/';

// px转rem
@function px2rem($px){
	@if(type-of($px) == 'number'){
		@return $px / $fontSizeBase * 1rem;		
	}
}

// 雪碧图定位
$imgW: 160px; // 雪碧图宽度
$imgH: 114px; // 雪碧图高度
@function bpspx($bgW, $x, $w){
	@if($bgW / 1px - $w / 1px == 0){
		@return 0;
	}
	@else{
		@return $x / ($bgW - $w) * 100%;
	}	
}
@function bpspy($bgH, $y, $h){
	@if($bgH / 1px - $h / 1px == 0){
		@return 0;
	}
	@else{
		@return $y / ($bgH - $h) * 100%;
	}	
}
@function bpss($bgW, $w){
	@return $bgW / $w * 100%;
}
%bps{
	background: url("#{$url}bg.png#{$version}") no-repeat;
}
@mixin bps($bgW, $bgH, $w, $h, $x, $y){ 
	@extend %bps; background-position: bpspx($bgW, $x, $w) bpspy($bgH, $y, $h); background-size: bpss($bgW, $w); width: px2rem($w); height: px2rem($h);
}
```
