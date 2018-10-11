之前皮肤开发了一个版本，抽是抽出来了，但是变量只抽出了几个颜色，没什么价值[（上个版本开发过程）](https://www.jianshu.com/p/ba1747714510)，
![、](https://upload-images.jianshu.io/upload_images/5077517-55e5a54891de85ef.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这次我又进行了一次迭代，现在是一个较成熟的版本了。整体理一下思路，可以总结为3步走和2层架构：

## 3步走

##### 第1步：抽取出皮肤相关样式
皮肤是样式的子集，想要做皮肤的管理，首先要把涉及到的样式都抽取出来，这里只涉及到了 登录页、考勤页、顶部菜单 3个部分。抽出来后放在assets/skin下。

![](https://upload-images.jianshu.io/upload_images/5077517-4bb873e4c0c25280.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/5077517-53fe2c3ce08709ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

也是分成了3个文件管理
##### 第二步： 抽取其中的变量
单抽出样式来肯定不够，要做配置化，需要从样式中抽出变化的值作为变量来管理，并且统一命名。

![](https://upload-images.jianshu.io/upload_images/5077517-c6a78363ea8151d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如图，也是对应3个section的3个文件。

命名方式是 sectionName-blockName{-status}-cssName

![](https://upload-images.jianshu.io/upload_images/5077517-b0572b5f12dbb8f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/5077517-bd8b08aeb2610cc2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

抽取出变量之后的less文件如下：

![](https://upload-images.jianshu.io/upload_images/5077517-f3fcc45e46ddeed9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样以后就只需要改动配置文件，而不需要修改样式文件了。
##### 第三步，抽取公共变量
配置中有很多同样的值，比如重复的颜色、重复的基础路径等。这些常量写了很多次，万一修改要修改n个地方，所以，我把这些散落的魔法值收集起来作为枚举值统一维护，使得配置变得更加的方便可控。

我抽取出了以下变量：

![](https://upload-images.jianshu.io/upload_images/5077517-ee5f58440ab1bd7e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/5077517-afda21e236b7709d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/5077517-8ff4f18a18faa3ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这里的颜色的命名我是按照色相和亮度来命名的，按照色相分为 红、橙、黄、红橙等，然后再加上深浅、亮暗的区分。虽然不是那么准确，但是能够简单区分了。

通过以上3个步骤，皮肤的可配置化就完成了。以后如果要开发一套新的皮肤，一般只需要改动配置就可以了。不过如果新皮肤有别的样式的更改，还是需要去修改样式文件，然后扩充配置变量的。随着皮肤开发的越来越多，配置也会越来越完善。

## 2层架构

经过上面3个步骤我们抽取出了皮肤样式和皮肤相关的配置变量，其实皮肤的架构也就分了这两层。

![](https://upload-images.jianshu.io/upload_images/5077517-03c552e2869648db.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


##  总结

皮肤是全部样式的一个子集，做到可配置需要3步：
1. 确定好范围之后，把样式抽取出来单独维护，
2.从中抽取抽变量来配置
3. 把一些颜色等常量值做成枚举的形式

整体的皮肤架构就分为**皮肤样式**和**皮肤配置**两层，架构图见上文。

[代码链接](https://github.com/lingxiaoguang/configed-skin/tree/master)






