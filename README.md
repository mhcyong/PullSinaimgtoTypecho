

#  新浪图床迁移至typecho助手

## ❗️❗️❗️请执行前一定要备份数据库，以免发生不可逆错误❗️❗️❗️

**因为自用的，代码写的比较随意，一些东西需要自己修改一下变量，下面都会提到**



## ❗️❗️❗️一些问题

#### 打开该接口一直空白加载等待页面？

目前的问题是PHP是阻塞式运行，在图片没有全部替换完成的时候是不会返回200响应，也就是浏览器是空白的等待加载状态，所以**耐心一点等**就可以了……

#### 如果文章中的新浪图床图片是代码块中内容，同样也会被替换？

确实是这样，不过一般新浪图床图片都是当做资源图片的吧

#### 保存到本地的图片错误 0kb？

请保证typecho的`usr/upload`下面的`sina`文件夹是可写的，你可以尝试手动新建这样的文件夹。


## 介绍

迁移内容包括：

* 文章 contens
* 独立页面 
* 评论
* 字段
* 设置（包括外观设置和后台设置项中）

**图片会被迁移至typecho的`usr/upload`下面的`sina`文件夹，并自动替换数据库中相应的地址。**

**对于代码块中的新浪图床图片则不会替换。**

## 使用方法

* 1.下载`Pull.php` 复制到你的博客主题文件夹下（无所谓什么主题都可以）
* 2.打开当前主题目录下面的的`function.php` 文件，在头部里面加上以下代码

```php
require_once("Pull.php");
```

* 3.访问下面地址查看你的博客含有新浪图片列表：

```
https://xxx.com/?action=pullsina&key=[在pull.php文件中自己修改$GLOBALS['key']变量的值]

//如我自己的博客
https://www.ihewro.com/?action=pullsina&key=ihewro
```

* 4.修改`Pull.php`的`$GLOBALS['is_replace']`为`true`，保存后重新调用接口。（**如果需要替换的图片数目很多，可以修改`$GLOBALS['limit']`变量限制每次调用接口的替换图片的数目，然后多次调用即可**）

**❗️❗️❗️任务进行中，请勿刷新或者关闭页面，否则会中断任务❗️❗️❗️**

**❗️❗️❗️使用结束后请务必及时删除该文件，避免接口被滥用❗️❗️❗️**

> 如果真的不小心刷新或关闭了也没太大关系，再次调用接口即可，但是还是尽量避免这种情况

## 相关

❗️该方法会导致评论无法判断来源referrer导致无法评论❗️[~~微博图床禁止外链的临时解决办法~~](https://www.willnet.net/index.php/archives/141/)


[新浪图床是不是不给用了 我调用的图片都是 403 了](https://www.v2ex.com/t/558239)


