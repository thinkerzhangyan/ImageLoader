# ImageLoader
自己练习码的[《Android开发艺术探索》][1]上的轻量级的ImageLoader和利用其实现的照片墙效果。

**ImageLoader**主要实现了：

> * 内存缓存
> * 硬盘缓存
> * 网络拉取
> * 同步加载
> * 异步加载
> * 图片压缩

同时ImageLoader解决了ListView，GridView滑动过程中的ImageView的复用问题。

**照片墙**的效果：


![此处输入图片的描述][2]
 

照片墙实现中优化了列表的卡顿，主要通过以下三个方面：

> * 不要在getView中执行耗时的操作，将加载图片的操作通过异步方式实现；

> * 控制异步任务的执行频率，当用户刻意的上下滑动列表的时候，会产生大量的异步的操作，这些异步任务会带来线程池的拥堵，同时随后会带来大量的UI更新操作，由于大量的UI更新操作同时发生，同时这些更新操作是发生在主线程中的，这会造成一定程度的卡顿。为了解决这个问题，我们可以考虑在列表滑动的时候，停止加载图片，当滑动停止时再加载图片，具体实现是通过给GridView设置onScrollStateChanged监听。

> * 开启硬件加速， android:hardwareAccelerated="true"。

具体实现，请阅读代码。

[1]: https://book.douban.com/subject/26599538/
[2]: http://ogts8rw5s.bkt.clouddn.com/zhaopianqiang.png
