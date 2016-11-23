# sass
sass使用方法
##SASS提供四个编译风格的选项：
　　* nested：嵌套缩进的css代码，它是默认值。<br>
　　* expanded：没有缩进的、扩展的css代码。<br>
　　* compact：简洁格式的css代码。<br>
　　* compressed：压缩后的css代码。<br>
  
+ sass监听某个文件变化
    sass --watch input.scss:output.css
+ sass监听文件夹变化
    sass --watch app/sass:public/stylesheets

###基本用法
+ 变量
  * $red:#f00;
  * $direction:left;  ->  div{border-#{$direction}-radius:5px;}
+ 计算
    * div{position:absolute;top:50px+$size;left:$size*2;}
+ 嵌套
    * div h1{margin:0;}<br>
    * div{ h1{margin:0;} }<br>
    //属性也可以嵌套，属性后面加上冒号
    * h1{ margin:{left:0;} } <br>
     //嵌套的代码块内，可以使用&引用父元素
    * a { &:hover { color: red; } }<br>
+ 注释
    * 标准的CSS注释 /* comment */ ，会保留到编译后的文件
    * 单行注释 // comment，只保留在SASS源文件中，编译后被省略
    * 在/*后面加一个感叹号，表示这是"重要注释"。即使是压缩模式编译，也会保留这行注释
+ 代码的重用
    * 继承
      .cla{border:1px solid red;}
      //clb继承cla,使用@extend
      .clb{ @extend .cla; width:100px; }
    * Mixin
      * 简单调用
      @Mixin left{ float:left; }
      div{ @include left; }
      * 指定参数
      @mixin right($value: 10px) {margin-right: $value;}
      div{ @include right(20px);}
    * 函数
      * SASS提供了一些内置的颜色函数<br>
        * rgb($red,$green,$blue)：根据红、绿、蓝三个值创建一个颜色；<br>
        * red($color)：从一个颜色中获取其中红色值；<br>
        * mix($color-1,$color-2,[$weight])：把两种颜色混合在一起。<br>
        * lighten(#cc3, 10%) // #d6d65c<br>
      * 字符串函数<br>
        * unquote()函数 //主要是用来删除一个字符串中的引号，如果这个字符串没有带有引号，将返回原始的字符串<br>
        * quote()函数   //刚好与  unquote()  函数功能相反，主要用来给字符串添加引号<br>
        * To-upper-case()函数 //将字符串小写字母转换成大写字母<br>
        * To-lower-case()函数 //大写变小写<br>
      * 数字函数<br>
        * percentage($value)：将一个不带单位的数转换成百分比值；<br>
        * ceil($value)；floor($value)；round($value)；abs($value)；min($numbers…)；max($numbers…)；random()；//等同javascript的Math函数
      * 列表函数<br>
        * length($list)：返回一个列表的长度值；length(10px 20px (border 1px solid) 2em)//4<br>
        * nth($list, $n)：返回一个列表中指定的某个标签值；nth((Helvetica,Arial,sans-serif),2)//Arial<br>
        * join($list1, $list2, [$separator])：将两个列给连接在一起，变成一个列表；join(10px，20px)//10px 20px<br>
        * append($list1, $val, [$separator])：将某个值放在列表的最后；append((10px,20px),30px)//10px 20px 30px<br>
        * zip($lists…)：将几个列表结合成一个多维的列表；zip(1px 2px,solid dashed,green blue)//1px solid green 2px dashed blue<br>
        * index($list, $value)：返回一个值在列表中的位置值。index(1px solid red, solid)//2<br>
      * Introspection函数<br>
        * type-of($value)：返回一个值的类型；type-of(1 / 2 = 1)//string  type-of(#fff)//color<br>
        * unit($number)：返回一个值的单位；unit(1em)//em  unit(10px / 3em)//px/em<br>
        * unitless($number)：判断一个值是否带有带位；unitless(100px)//false  unitless(100)//true<br>
        * comparable($number-1, $number-2)：判断两个值是否可以做加、减和合并；comparable(2px,1px)//true  comparable(2px,1%)//false<br>
      * Miscellaneous函数
        * if(true,1px,2px)//1px  if(false,1px,2px)//2px
    * 插入文件
      @import "path/filename.scss";<br>
      //如果插入的是css文件则等同于css的import
+ 高级用法  
    * 条件语句<br>
      div{ @if 1 + 3 >= 2 { border: 1px solid; } }<br>
      @if lightness($color) > 30% { color: #000; } <br>
      @else { color: #fff; }
    * 循环语句
      * for 
         @for $i from 1 to 10 { .border-a#{$i} { border: #{$i}px solid blue; } }
      * while
         $i: 6;
         @while $i > 0 { .border-a#{$i} { border:#{$i}px solid blue; }$i: $i - 1; }
      * each
         @each $member in a, b, c, d { .img-#{$member} { background-image: url("/image/#{$member}.jpg");} }  
    * 自定义函数<br>
       @function double($n) { @return $n * 2; }
       \#sidebar { width: double(5px); }
