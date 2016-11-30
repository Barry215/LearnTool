## Android 知识流

### UI

#### 生成Dialog

```java
public void showHostDialog(){
        View textEntryView = LayoutInflater.from(this).inflate(R.layout.alert_edittext, null);
        final EditText editText = (EditText) textEntryView.findViewById(R.id.et_content);

        String host = SharedPreferenceUtils.getString(this, "system_host", "");
        editText.setText(host);

        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setCancelable(true);
        builder.setView(textEntryView);
        builder.setTitle("HOST配置");
        builder.setMessage("配置hosts，以空格分隔，每行一个");
        builder.setPositiveButton("确认", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
                imm.hideSoftInputFromWindow(editText.getWindowToken(), 0);
                SharedPreferenceUtils.putString(MainActivity.this, "system_host", editText.getText()+"");
                DeviceUtils.changeHost(((SysApplication)getApplication()).proxy,editText.getText()+"");
            }
        });
        builder.setNegativeButton("清空", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
                imm.hideSoftInputFromWindow(editText.getWindowToken(), 0);
                SharedPreferenceUtils.putString(MainActivity.this, "system_host", "");
                DeviceUtils.changeHost(((SysApplication)getApplication()).proxy,editText.getText()+"");
            }
        });
        builder.show();
    }
}
```

alert_edittext.xml

```xml
<?xml version="1.0" encoding="utf-8"?>


<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal" android:layout_width="match_parent"
    android:layout_height="match_parent">

        <EditText
            android:textSize="14sp"
            android:layout_marginLeft="20dp"
            android:layout_marginRight="20dp"
            android:id="@+id/et_content"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="127.0.0.1 www.darkal.cn"/>

    </LinearLayout>

```



#### RecyclerView

[揭开RecyclerView的神秘面纱(一)：RecyclerView的基本使用](http://www.jianshu.com/p/626a082bf569)

[揭开RecyclerView的神秘面纱(二)：处理RecyclerView的点击事件](http://www.jianshu.com/p/f2e0463e5aef)

[揭开RecyclerView的神秘面纱(三)：操作数据及添加分割线](http://www.jianshu.com/p/a3aac86523d2)

[简单易用的 RecyclerView.Adapter 封装库](http://www.open-open.com/lib/view/open1479518526643.html)

[完美解决隐藏Listview和RecyclerView去掉滚动条和滑动到边界阴影的方案](http://www.voidcn.com/blog/ming2316780/article/p-5999345.html)



#### 轮播图

[Android 实现带指示器的自动轮播式ViewPager](http://www.jianshu.com/p/ae56545ec7e2)



#### ToolBar

[Android ToolBar 使用完全解析](http://www.jianshu.com/p/ae0013a4f71a)



#### LayoutInflater

[LayoutInflater用法](http://blog.csdn.net/xsf50717/article/details/49446687)

[LayoutInflater和inflate方法的用法](http://blog.csdn.net/robertcpp/article/details/51523218)



#### TabLayout

[Design库-TabLayout属性详解](http://www.jianshu.com/p/2b2bb6be83a8)

[Material Design：TabLayout的使用](http://www.jianshu.com/p/9c072bc99ebe)

[TabLayout实现滑动标签页](http://blog.csdn.net/rosechan/article/details/51568130)

 [去掉TabLayout下的阴影，AppBarLayout下的阴影](http://blog.csdn.net/dreamsever/article/details/52672739)



#### ViewPager

[FragmentPagerAdapter和FragmentStatePagerAdapter区别](http://blog.csdn.net/dreamzml/article/details/9951577)



#### CoordinatorLayout

[使用CoordinatorLayout打造一个炫酷的详情页](http://www.jianshu.com/p/5287d090e777)

[一个神奇的控件——Android CoordinatorLayout与Behavior使用指南](http://www.jianshu.com/p/488283f74e69)



#### Bottom Sheet

[三分钟玩转Android Bottom Sheet](http://www.jianshu.com/p/e9e9931c510c)

[使用Bottom Sheet实现底部菜单](http://www.jianshu.com/p/1024ad202683)

[BottomSheets的使用](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2016/0228/4008.html)

[Android Bottom Sheet详解](http://blog.csdn.net/qibin0506/article/details/51002241)



#### SwipeRefreshLayout

[Android开发之SwipeRefreshLayout实现下拉刷新](http://www.jianshu.com/p/97ab87cfce47)



### UI效果

#### 搜索框

[[译]Android Material 搜索框实现详细说明](http://www.jianshu.com/p/24dff5073e2c)



#### RecyclerView左右滑动

[仿知乎的侧滑删除](http://blog.csdn.net/tyk0910/article/details/51669205)

[RecyclerView侧滑菜单，RecyclerView滑动删除，RecyclerView长按拖拽](http://www.jianshu.com/p/3ea18300f40c) ✨

[RecyclerView的拖动、滑动删除](https://segmentfault.com/a/1190000005645907)



#### 在列表滚动的时候显示/隐藏View

[让 Toolbar 随着 RecyclerView 的滚动而显示 / 隐藏](http://gold.xitu.io/entry/56cd9c9dd342d30054ca35b8?utm_source=gold-miner&utm_medium=readme&utm_campaign=github)



#### 底部弹窗

[使用 DialogFragment 实现底部弹窗布局](http://www.wangchenlong.org/2016/08/07/1608/076-bottom-dialog-fragment/)



### 传输

#### FlatBuffer

[数据交换格式FlatBuffers介绍](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0831/3395.html)



### 图片加载

#### Glide

##### 应用

[GlideBitmapPool](https://github.com/amitshekhariitbhu/GlideBitmapPool)



### Android生命周期

[分析 Activity 的生命周期](http://www.wangchenlong.org/2016/02/23/1603/235-activity-lifecycle/)



### Android启动模式

[分析 Activity 的启动模式](http://www.wangchenlong.org/2016/02/23/1603/234-activity-launch-mode/)



### Fragment生命周期

[Fragment的理解, Fragment的生命周期](http://www.jianshu.com/p/6095b626069c)



### 调用系统图册和相机

[Android实现用户头像更换，包括调用相机和系统相册，并裁剪返回](https://github.com/ZhouCP/PhotoDemo)



### Markdown

[可以加载md的webview](https://github.com/falnatsheh/MarkdownView)

[Android Markdown编辑器](https://github.com/qinci/MarkdownEditors)

[Android平台下的富文本解析器，支持Html和Markdown](https://github.com/zzhoujay/RichText)

[Android平台下的原生Markdown解析器](https://github.com/zzhoujay/Markdown)

[上面的博文解释](http://blog.csdn.net/u014608640/article/details/53080027)





### 异步

#### RxJava

[给 Android 开发者的 RxJava 详解](https://gank.io/post/560e15be2dca930e00da1083) ✨

[大头鬼的Rxjava译文](http://blog.csdn.net/lzyzsd/article/category/2767743)

##### 操作符

[高大上的操作符说明](http://mrfu.me/2016/01/10/RxWeekend/#tips7)

[操作符分类](https://mcxiaoke.gitbooks.io/rxdocs/content/Operators.html)

##### demo

[RxJava 2 Android Examples](https://github.com/amitshekhariitbhu/RxJava2-Android-Samples)



### 网络框架

#### OkHttp

[OkHttp3的基本用法](http://www.jianshu.com/p/1873287eed87)

#### Retrofit

[Retrofit2.0使用详解](http://blog.csdn.net/ljd2038/article/details/51046512)

[Retrofit使用指南(内含请求日志打印)](http://www.jianshu.com/p/91ac13ed076d) ✨

[Retrofit的json传输,文件下载和上传](http://blog.csdn.net/jiangxuqaz/article/details/50759239) ✨

[小白进阶回忆录：Retrofit2要点梳理](http://www.jianshu.com/p/dd2804030b89)✨

[Retrofit基本用法和流程分析](http://www.jianshu.com/p/94ca8a284ebb)



### 账号验证

#### AccountManager

[android账号创建，管理，同步](http://www.jianshu.com/p/c9337be547ae)



### 注解

#### Dagger2

[Dagger2 使用详解](http://www.jianshu.com/p/94d47da32656)



### 即时通讯

[源码提供！Android即时通讯和sns开源项目汇总](http://www.jianshu.com/p/b2ca52337fe5)



### 蓝牙

[普通蓝牙EDR连接，BLE蓝牙连接,示例，操作蓝牙打印机demo](https://github.com/vir56k/bluetoothDemo)



### 发布APK

 [Android Studio如何发布APK](http://blog.csdn.net/u014608640/article/details/53034916)



### 集成功能

#### 支付

[Android微信支付爬坑](http://www.open-open.com/lib/view/open1479350904960.html)



## Android Studio

#### 教程

[Android Studio教程从入门到精通](http://www.open-open.com/lib/view/open1433387390635.html)

[Android Studio 使用推荐](http://www.open-open.com/lib/view/open1475497562965.html)



#### AS 2.2 新特性

[汇总Android Studio 2.2 给我们带来的十大新功能](http://www.open-open.com/lib/view/open1474534858979.html)



#### Mac 快捷键

[AndroidStudio常用快捷键(Mac)](https://github.com/GcsSloop/AndroidNote/blob/master/ChaosCrystal/AndroidStudio%E5%B8%B8%E7%94%A8%E5%BF%AB%E6%8D%B7%E9%94%AE(Mac).md)



#### 图片生成器

[Android神兵利器之Image Asset Studio](http://www.open-open.com/lib/view/open1477538222320.html)



#### 取消打开上次工程

[取消android studio启动时自动打开上次关闭的项目](http://blog.csdn.net/qq_20785431/article/details/51112582)



#### 离线Gradle配置

[mac 下 android studio 的离线gradle极速配置方法](http://www.cnblogs.com/thtlovelife/p/5872801.html)

[Mac下AndroidStudio中手动配置Gradle](http://www.jianshu.com/p/36e569c1bb12)

[最详细的mac下Android studio配置gradle的路径](http://blog.csdn.net/u013634213/article/details/51120783)



### 错误锦集

[Android Studio出现Error:No service of type Factory available in ProjectScopeServices](http://www.jianshu.com/p/c4f4894ad215)

[Error:Cause: com.android.sdklib.repository.FullRevision](http://blog.csdn.net/caiwenfeng_for_23/article/details/51167143)



### Demo效果

#### [AndroidHttpCapture](https://github.com/JZ-Darkal/AndroidHttpCapture)

> AndroidHttpCapture网络诊断工具 是一款针对于移动流量劫持而开发的手机抓包软件

具有的效果：

- Material Design效果弹出框
- 标准的设置页面
- 查看软件版本
- 悬浮球的上浮生成
- web浏览器嵌入
- Action Bar处的搜索框
- 二维码识别和扫描




#### [微阅](https://github.com/YiuChoi/MicroReader)

> 一个小而美的阅读客户端，包含微信精选，IT之家(去广告),果壳热门，知乎日报，和视频推荐栏目，每天更换主题。

采用的技术：

- Retrofit 的使用，包括使用 Http 缓存、converter 的使用等；
- RxJava 的使用，包括配合 Retrofit、RxBus 的使用等；
- MVP 架构实践，包括 presenter 的生命周期管理；
- RecycleView + CardView 的使用；
- 使用 Palette 从图片中取色；
- 主题动态切换；
- Android 4.4 及以上版本的状态栏适配；
- FloatingActionButton 的自定义动作；
- AppCompatActivity 配合 PreferenceFragment 实现 Material Design 的设置界面；
- WebView 的使用，包括显示加载进度条、播放视频等；
- VideoView 的使用，包括自定义按钮；
- 动态切换 NavigationView 的菜单项
- Android 抓包及逆向分析
- 数据离线缓存
- 使用Gradle多渠道打包及自定义编译的APK文件名
- Activity滑动返回的实现
- 夜间模式实践
- 最新版本获取
- 分享接口的实现




### 轮子

[A library for debugging android databases and shared preferences](https://github.com/amitshekhariitbhu/Android-Debug-Database)

> 安卓本地数据库的数据监控，可以通过同一局域网的浏览器来访问本地数据库



[A Complete Fast Android Networking Library that also support HTTP/2 ](https://github.com/amitshekhariitbhu/Fast-Android-Networking)

> 一个支持各种请求类型的网络库



[ViewPagerIndicator](https://github.com/LuckyJayce/ViewPagerIndicator)

>  Indicator 取代 tabhost，实现网易顶部tab，新浪微博主页底部tab，引导页，无限轮播banner等效果，高度自定义tab和特效



[GuideHelper](https://github.com/LuckyJayce/GuideHelper)

> 新手引导页，轻松的实现对应的view上面的显示提示信息和展示功能给用户



[LoadingLayoutDemo](https://github.com/weavey/LoadingLayoutDemo)

> 项目里都会遇到几种页面，分别为加载中、无网络、无数据、出错四种情况，经常要使用，所以封成库引用了



[Simple, pretty and powerful logger for android](https://github.com/orhanobut/logger)

> 安卓的日志方案



[Google百分比布局库的扩展](https://github.com/hongyangAndroid/android-percent-support-extend)

> 对于android-percent-support的扩展库



[RecyclerRefresh](https://github.com/leoleohan/RecyclerRefresh)

>Android使用SwipeRefreshLayout和RecyclerView实现仿简书下拉刷新和上拉加载更多



[BaseRecyclerViewAdapterHelper](https://github.com/CymChad/BaseRecyclerViewAdapterHelper)

> Powerful and flexible RecyclerAdapter，封装了很多用法



### 代码开源协议

[程序员需要了解的版权协议](https://github.com/GcsSloop/AndroidNote/blob/magic-world/ChaosCrystal/%E5%BC%80%E6%BA%90%E5%85%B1%E4%BA%AB%E5%8D%8F%E8%AE%AE.md)



### 安卓笔记

[AndroidNote](https://github.com/GcsSloop/AndroidNote)

[Android开发总结](https://github.com/JohnTsaiAndroid/AndroidTips)