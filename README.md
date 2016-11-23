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
    * div{
          h1{margin:0;}
        }<br>
     /*属性也可以嵌套，属性后面加上冒号*/ 
    * h1{
          margin:{left:0;}
        } <br>
     /*嵌套的代码块内，可以使用&引用父元素*/
    * a {&:hover { color: red; }}<br>
+ 注释
    * 标准的CSS注释 /* comment */ ，会保留到编译后的文件
    * 单行注释 // comment，只保留在SASS源文件中，编译后被省略
    * 在/*后面加一个感叹号，表示这是"重要注释"。即使是压缩模式编译，也会保留这行注释
+ 代码的重用
    * 继承
      .cla{border:1px solid red;}
      /*clb继承cla,使用@extend*/
      .clb{ @extend .cla; width:100px; }
    * Mixin
      /*简单调用*/
      @Mixin left{ float:left; }
      div{ @include left; }
      /*指定参数*/
      @mixin right($value: 10px) {margin-right: $value;}
      div{ @include right(20px);}
    * 颜色函数
      /*SASS提供了一些内置的颜色函数*/
       rgb($red,$green,$blue)：根据红、绿、蓝三个值创建一个颜色；
       red($color)：从一个颜色中获取其中红色值；
       mix($color-1,$color-2,[$weight])：把两种颜色混合在一起。
       lighten(#cc3, 10%) // #d6d65c
    * 插入文件
      @import "path/filename.scss";/*如果插入的是css文件则等同于css的import*/
+ 高级用法  
    * 条件语句
      div{ @if 1 + 3 >= 2 { border: 1px solid; } }
      @if lightness($color) > 30% { color: #000; } 
      @else { color: #fff; }
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
      
    
        
