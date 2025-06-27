<div style="background-color: white; width: 100vw; height: 100vh; margin: 0; padding: 0; overflow: hidden; position: relative;">
  <!-- 背景图片 -->
  <img src="/bgimages/6.26傍晚.jpg" 
       style="width: 100%; height: auto; display: block; 
              filter: blur(3px) brightness(0.8); 
              opacity: 0.9; /* 也可以用 opacity 微调透明感和亮度配合 3px越大越模糊，0.8降低亮度1是原图亮度*/" 
       alt="傍晚景色">
  <!-- 前景文字 -->
  <div style="text-align: center; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); color: black; font-size: 50px;">
    帮助网站   🎉🎉🎉

  </div>
</div>


<!--  
问：position: relative（父容器） + position: absolute（文字），让文字可以脱离图片层级，避免被滤镜影响；这是什么原理？  
答：一、核心原理：“层级分离”
一句话概括：通过不同的定位方式，让「图片 + 滤镜」和「文字」处于不同的 “层级空间”，滤镜就不会穿透影响到文字
可以类比成 “物理世界的分层画板”：
父容器开了一个 “画布”（position: relative 搭建基础画板 ）
图片是 “底层画布”，你给它加了滤镜（相当于在底层画画 + 特效）
文字是 “上层贴纸”，用 position: absolute 贴到画布上方，和底层画布分离
二、分步拆解
1. 父容器 position: relative 的作用
给父元素设置 position: relative 后，它会创建一个 “局部层叠上下文”，相当于在页面里划分一块 “独立小天地”。
这个小天地里的子元素，如果用 position: absolute，会以这个父容器为参考坐标系（而不是整个页面），方便精准定位。
1. 图片 position: static（默认值）
图片默认是 position: static，会老老实实待在父容器的 “文档流” 里，此时给它加 filter: blur()，就像给 “底层画布” 涂了模糊特效。
1. 文字 position: absolute 的魔法
当文字用 position: absolute 时，它会脱离默认的文档流，相当于从 “底层画布” 上揭下来，贴到一个 “上层透明层”。
因为它的参考系是 position: relative 的父容器，所以能精准放在父容器的任意位置（比如 top: 50px; left: 50px ）。
关键：这个 “上层透明层” 和 “底层画布（带滤镜的图片）” 是分离的层级，滤镜只会影响底层，不会穿透到上层文字！
1. 层叠上下文的 “隔离” 效果
每个 position: relative/absolute/fixed 等定位，都会影响元素的层叠顺序（z-index）。
父容器的 relative 相当于给子元素划定了一个 “层级范围”，文字的 absolute 虽然脱离文档流，但依然在父容器的层级体系内，和带滤镜的图片自然分层。
三、类比生活场景理解
想象你在做手工：
拿一块玻璃（父容器 relative ），这是基础底板。
在玻璃背面贴一张照片（图片 static ），然后给照片喷一层模糊喷雾（filter: blur ）。
最后在玻璃正面贴一张透明贴纸写文字（文字 absolute ）。
此时：
模糊喷雾（滤镜）只影响玻璃背面的照片（底层图片）
玻璃正面的贴纸文字（上层绝对定位）完全不受影响！
四、关键总结
position: relative（父） → 建一个 “局部层级容器”，给子元素当定位参考
position: absolute（文字） → 让文字脱离底层文档流，跳到 “上层透明层”
结果：滤镜只作用于底层图片，文字因为在独立上层，完美避开滤镜影响
这就是 CSS 定位和层叠上下文的巧妙配合，实现 “滤镜只改背景，不影响文字” 的核心逻辑～
-->