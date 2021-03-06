Web加载过程优化方案	
=============

移动Web加载速度受限于移动网络，移动网络的特点是不够稳定。所以移动Web在开发的时候就需要注意将页面制作的尽量小。同时为了满足不稳定的网络环境而优化。以下是关于加载优化的一些具体建议。

## 优化目标
1. 传输内容越少越好。
2. 内容较少的情况下，请求数越少越好。压缩后每个请求传输的内容应大于20K。

## 服务器配置

1. 对文本内容开启gzip压缩。
2. 开启keep-alive保持长连接，建议keep-alive大于5s.
3. 对于https协议，打开ssl session,减少再次连接时长。

## 开发
1. 使用为移动端优化的较小的基础库，例如使用zepto替代jquery, 对于不需要的功能，从库里移除.
2. 不要使用过大的图片，对于可以用CSS实现的效果，使用CSS实现。大面积的图片，可以使用矢量图的，建议使用矢量图，例如SVG。
3. 尽量合并请求，包括合并css/js、 使用雪碧图。
4. 使用发布工具压缩代码，合并文件，去掉多除的注释、空白，精简JS变量名。

## 释疑
1. 为什么请求数越少越好？多连接并行加载不是会更快吗？
  - 经过实测，3G/4G条件下，每个请求的连接耗时特别长，对于30K的内容，连接耗时超过1/3左右。 原因是运营商对上行大包、小包的转发优先策略不一样，一般运营商会配置小包优先策略，发HTTP请求的TCP包耗时远超普通的TCP回包。

