动画
.box img {
  animation: rotateFC 4s;
}

@keyframes rotateFC {
  0% {
    transform: rotate(0deg);
  }
  25% {
    transform: rotate(120deg);
  }
  100% {
    transform: rotate(0deg);
  }
}
         
            
动画的拆分
animation: move 4s linear 1s infinite forwards alternate ;*/

animation-name: move;
animation-duration: 2s;
animation-timing-function: ease;    ease linear ease-in ease-in-out ease-out 
animation-delay: 1s;
animation-fill-mode: forwards;           /*动画结束的时候的状态 forwards 保持结束状态  backwards 回答最原生的状态 没有动画的那个状态*/
animation-iteration-count: infinite;  动画执行的次数
animation-direction: alternate;       /*动画逆播放*/
                /*分步执行 steps(3)*/
               }

.box:hover {
         animation-play-state: paused;          /*执行的状态 是执行中  暂停  running、paused*/
 } 

### transition 和 animation 的区别
transition的优点在于简单易用，但是它有几个很大的局限。 
（1）transition需要事件触发，所以没法在网页加载时自动发生。 
（2）transition是一次性的，不能重复发生，除非一再触发。 
（3）transition只能定义开始状态和结束状态，不能定义中间状态，也就是说只有两个状态。 
（4）一条transition规则，只能定义一个属性的变化，不能涉及多个属性。 
CSS Animation就是为了解决这些问题而提出的。

CSS3的animation制作动画效果主要包括两部分：1. 用关键帧声明一个动画，2.在animation调用关键帧声明的的动画。

animation属性类似于transition，他们都是随着时间改变元素的属性值，其主要区别在于：transition需要触发一个事件才会随着时间改变其CSS属性；animation在不需要触发任何事件的情况下，也可以显式的随时间变化来改变元素CSS属性，达到一种动画的效果
