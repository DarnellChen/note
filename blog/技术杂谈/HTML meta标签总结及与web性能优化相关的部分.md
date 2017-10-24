# HTML meta标签总结及与web性能优化相关的部分

## 参考博文
> [HTML meta标签总结与属性的使用介绍](http://www.imooc.com/article/4475)

> [META http-equiv 大全](http://www.cnblogs.com/jerryshi/archive/2008/10/14/1310611.html)

> [web性能优化之：no-cache与must-revalidate深入探究](http://www.cnblogs.com/chyingp/p/no-cache-vs-must-revalidate.html)

## 综合整合

### name属性
  
* keywords  网页关键字
* description 网站内容描述
* viewport  移动端窗口形式
* robots  定义搜索引擎爬虫的索引方式
```
    <meta name="robote" content="none">
    
    1.none : 搜索引擎将忽略此网页，等价于noindex，nofollow。
    2.noindex : 搜索引擎不索引此网页。
    3.nofollow: 搜索引擎不继续通过此网页的链接索引搜索其它的网页。
    4.all : 搜索引擎将索引此网页与继续通过此网页的链接索引，等价于index，follow。
    5.index : 搜索引擎索引此网页。
    6.follow : 搜索引擎继续通过此网页的链接索引搜索其它的网页。
```
* author  标注网页作者
* generator 标注开发软件
* copyright 标注版权
* revisit-after 设置搜索引擎爬虫重访时间
* renderer 在双核浏览器下选择渲染方式
```
    <meta name="renderer" content="webkit"> //默认webkit内核 
    <meta name="renderer" content="ie-comp"> //默认IE兼容模式 
    <meta name="renderer" content="ie-stand"> //默认IE标准模式
```

### http-equiv属性
```
  语法格式
  <meta http-equiv="参数" content="具体的描述">
```
* content-Type和Content-Language 设定网页字符集
* X-UA-Compatible 告诉浏览器用什么版本进行渲染
```
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/> //指定IE和Chrome使用最新版本渲染当前页面
```
* cache-control 指定缓存机制
* expires 网页到期时间，一旦网页过期，必须到服务器上重新调阅。
* refresh 设定自动刷新并调向设定的网址
```
  <Meta http-equiv=”Refresh” Content=”30″>    刷新自己

  <Meta http-equiv=”Refresh” Content=”5; Url=http://www.downme.com”>    跳转到指定页面
```
* Set-Cookie  cookie设定
* Pragma 禁止浏览器从本地机的缓存中调阅页面内容。
* Page-Enter、Page-Exit 这个是页面被载入和调出时的一些特效。
```
  <Meta http-equiv=”Page-Enter” Content=”revealTrans(duration=x, transition=y)”>

  <Meta http-equiv=”Page-Exit” Content=”revealTrans(duration=x, transition=y)”>

    Duration表示滤镜特效的持续时间(单位：秒)

    Transition滤镜类型。表示使用哪种特效，取值为0-23。

    0 矩形缩小 1 矩形扩大 2 圆形缩小 3 圆形扩大 4 下到上刷新 
    5 上到下刷新 6 左到右刷新 7 右到左刷新 8 竖百叶窗 9 横百叶窗 
    10 错位横百叶窗 11 错位竖百叶窗 12 点扩散 13 左右到中间刷新 14 中间到左右刷新 
    15 中间到上下 16 上下到中间 17 右下到左上 18 右上到左下 19 左上到右下 
    20 左下到右上 21 横条 22 竖条 23 以上22种随机选择一种
```
