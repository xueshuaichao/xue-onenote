所谓GPU，就是图形处理器的缩写，相当于PC中的显卡。手机中的GPU也是为了对图形、图像处理而存在的，所谓强制渲染，就是hwa（hardware acceleration硬件加载）的一种，其存在的意义就是为了分担cpu的负担，其原理是通过GPU对软件图形的处理来减轻CPU的负担。从而使应用软件能够以更快的速度被处理，以达到提速的目的。

### 1.何为硬件加速
就是将浏览器的渲染过程交给GPU处理，而不是使用自带的比较慢的渲染器。这样就可以使得animation与transition更加顺畅
我们可以在浏览器中用CSS开启硬件加速，使GPU发挥功能，从而提升性能
浏览器接收到页面文档后，会将文档中的标记语言解析为DOM树。DOM树和CSS结合后形成浏览器构建页面的渲染树。渲染树中包含大量的渲染元素，每个渲染元素会被分到一个图层中，每个图层又会被加载到GPU形成渲染纹理，而图层在GPU中transform是不会触发repaint的，最终这些使用transform的图层都会由独立的合成器进程进行处理
CSS transform会创建了一个新的复合图层，可以被GPU直接用来执行transform操作。
### 浏览器什么时候会创建一个独立的复合图层呢？事实上一般是在以下几种情况下：
3D或者CSS transform
<video>和<canvas>标签
css filters
元素覆盖时，比如使用了z-index属性

### 为什么硬件加速会使页面流畅
因为transform属性不会触发浏览器的repaint（重绘），而绝对定位absolute中的left和top则会一直触发repaint（重绘）。
### 为什么transform没有触发repaint呢？
简而言之，transform动画由GPU控制，支持硬件加载，并不需要软件方面的渲染。
并不是所有的CSS属性都能触发GPU的硬件加载，事实上只有少数的属性可以，比如transform、opacity、filter
### 如何在桌面和移动端用CSS开启硬件加速
CSS animations、transforms以及transitions不会自动开启GPU加速，而是由浏览器的缓慢的软件渲染引擎来执行，那我们怎样才可以切换到GPU模式呢，很多浏览器提供了某些触发的CSS规则。
现在，像Chrome、Firefox、Safari，IE9+和最新版本的Opera都支持硬件加速，当他们检测到页面中某个DOM元素应用了某些CSS规则时就会开启，最显著的特征的元素是3D变化。

.cube{
    -webkit-transform:translate3d(250px,250px,250px);
    rotate3d(250px,250px,250px,-120deg)
    scale3d(0.5,0.5,0.5);
}

可是在一些情况下，我们并不需要对元素应用3D变换的效果，那怎么办呢？这时候我们可以使用个小技巧“欺骗”浏览器来开启硬件加速。
虽然我们可能不想对元素应用3D变换，可我们一样可以开启3D引擎。例如我们可以用transform: translateZ(0); 来开启硬件加速 。
.cube {
   -webkit-transform: translateZ(0);
   -moz-transform: translateZ(0);
   -ms-transform: translateZ(0);
   -o-transform: translateZ(0);
   transform: translateZ(0);
   /* Other transform properties here */
}

在 Chrome and Safari中，当我们使用CSS transforms 或者 animations时可能会有页面闪烁的效果，下面的代码可以修复此情况：
.cube {
   -webkit-backface-visibility: hidden;
   -moz-backface-visibility: hidden;
   -ms-backface-visibility: hidden;
   backface-visibility: hidden;
 
   -webkit-perspective: 1000;
   -moz-perspective: 1000;
   -ms-perspective: 1000;
   perspective: 1000;
   /* Other transform properties here */
}

在webkit内核的浏览器中，另一个行之有效的方法是
.cube {
   -webkit-transform: translate3d(0, 0, 0);
   -moz-transform: translate3d(0, 0, 0);
   -ms-transform: translate3d(0, 0, 0);
   transform: translate3d(0, 0, 0);
  /* Other transform properties here */
}
原生的移动端应用(Native mobile applications)总是可以很好的运用GPU，这是为什么它比网页应用(Web apps)表现更好的原因。硬件加速在移动端尤其有用，因为它可以有效的减少资源的利用(麦时注：移动端本身资源有限)。
### 总结
只对我们需要实现动画效果的元素应用以上方法，如果仅仅为了开启硬件加速而随便乱用，那是不明智的。
小心使用这些方法，如果通过你的测试，结果确是提高了性能，你才可以使用这些方法。使用GPU可能会导致严重的性能问题，因为它增加了内存的使用，而且它会减少移动端设备的电池寿命。

### 使用硬件加速的问题
1. 内存。如果CPU加载了大量的纹理，那么很容易就会发生内容问题，这一点在移动端浏览器上尤为明显，所以，一定要牢记不要让页面的每个元素都使用硬件加速
2. 使用GPU渲染会影响字体的抗锯齿效果，这是因为GPU和CPU的具有不同的渲染机制。即使最终硬件加速停止了，文本还是会在动画期间显示得很模糊。
