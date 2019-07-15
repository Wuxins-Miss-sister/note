```js
//p12标签宽度
$p12:16px;
$textAlign: right;
$font-family: PingFangSC-Regular;
$letter-spacing: 0;
@mixin p12($num) {
  width: $num * $p12;
  // width: 
}
//text
@mixin p($color,$size,$textAlign,$font-family,$letter-spacing:0,$num) {
  font-family: $font-family;
  width: $num * $p12;
  font-size: 12px;
  color: $color;
  letter-spacing: $letter-spacing;
  text-align: $textAlign;
}
@mixin div($background,$line-height,$height,$width:''){
  height: $height;
  width: $width;
  line-height: $line-height;
  background: $background;
}
@mixin border($color:'black',$width:'1px',$background:'',$linetype:solid){
  border:$color $linetype $width;
}
@mixin margin($top,$left,$bottom,$right) {
  margin: $top $left $bottom $right;
}
@mixin padding($top, $left, $bottom, $right) {
  padding: $top $left $bottom $right;
}
```

