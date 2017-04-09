## Android 知识流

### Android 教程

[Android官方培训课程中文版](https://github.com/kesenhoo/android-training-course-in-chinese)

[android sdk 源码解析](https://github.com/LittleFriendsGroup/AndroidSdkSourceAnalysis)

[掘金翻译计划](https://github.com/xitu/gold-miner)



### UI

#### Android 图标网站

[Android Material 材料风格图标LOGO生成器](http://jaqen.me/mdpub/)



#### 自定义View

[Android自定义view详解](http://shaohui.me/2016/07/08/Android%E8%87%AA%E5%AE%9A%E4%B9%89view%E8%AF%A6%E8%A7%A3/)



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

[RecyclerView:实现带header的grid](http://www.open-open.com/lib/view/open1437662138631.html)

[RecyclerView下拉刷新上拉加载](http://ittiger.cn/RecyclerView%E4%B8%8B%E6%8B%89%E5%88%B7%E6%96%B0%E4%B8%8A%E6%8B%89%E5%8A%A0%E8%BD%BD.html)

[对RecyclerView Item做动画](https://ruzhan123.github.io/2016/07/01/2016-07-01-01-%E5%AF%B9RecyclerViewItem%E5%81%9A%E5%8A%A8%E7%94%BB/)



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

[A Material Design ViewPager easy to use library](https://github.com/florent37/MaterialViewPager)



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



#### TextView

[TextView 实战之你真的懂我么？](http://blog.csdn.net/sdkfjksf/article/details/51317204)



#### TextInputLayout

[TextInputLayout 完全解析](http://m.blog.csdn.net/article/details?id=51957305)

[【Android-UI】TextInputLayout的使用](http://m.blog.csdn.net/article/details?id=52193802)

[EditText辅助控件—TextInputLayout](http://www.jianshu.com/p/9ad85a9fbfd4)

[使用TextInputLayout创建一个登陆界面](http://www.jcodecraeer.com/a/basictutorial/2015/0821/3338.html)



#### Spinner

[nice-spinner](https://github.com/arcadefire/nice-spinner)

[android-spinnerwheel](https://github.com/ai212983/android-spinnerwheel)

[Material-Spinner](https://github.com/jaredrummler/Material-Spinner)

[BetterSpinner](https://github.com/Lesilva/BetterSpinner)



#### FloatingActionButton

[FloatingActionButton](https://github.com/Clans/FloatingActionButton)

[BoomMenu](https://github.com/Nightonke/BoomMenu)



#### Webview

[用js调用安卓接口](http://blog.csdn.net/a153614131/article/details/50353256)



### UI效果

#### 搜索框

[[译]Android Material 搜索框实现详细说明](http://www.jianshu.com/p/24dff5073e2c)



#### 底部对话框

[BottomDialog](https://github.com/shaohui10086/BottomDialog)



#### 底部bar

[Material-BottomNavigation](https://github.com/sephiroth74/Material-BottomNavigation)



#### 列表加载更多

[VistaReyclerView](https://github.com/shaohui10086/VistaReyclerView)



#### ViewPager

[听说你想用ViewPager实现这样的效果](http://www.jianshu.com/p/eaea9eb2e80c)



#### RecyclerView左右滑动

[仿知乎的侧滑删除](http://blog.csdn.net/tyk0910/article/details/51669205)

[RecyclerView侧滑菜单，RecyclerView滑动删除，RecyclerView长按拖拽](http://www.jianshu.com/p/3ea18300f40c) ✨

[RecyclerView的拖动、滑动删除](https://segmentfault.com/a/1190000005645907)

[左右滑动库](https://github.com/vcalvello/SwipeToAction)

[AndroidSwipeLayout](https://github.com/daimajia/AndroidSwipeLayout)



#### 实现 Toolbar 随着 RecyclerView 的滚动而显示 / 隐藏 的效果

[让 Toolbar 随着 RecyclerView 的滚动而显示 / 隐藏](http://gold.xitu.io/entry/56cd9c9dd342d30054ca35b8?utm_source=gold-miner&utm_medium=readme&utm_campaign=github)



#### Behavior

[自定义Behavior的艺术探索-仿UC浏览器主页](http://www.jianshu.com/p/f7989a2a3ec2)

[BehaviorDemo](https://github.com/CSnowStack/BehaviorDemo)



#### 底部弹窗

[使用 DialogFragment 实现底部弹窗布局](http://www.wangchenlong.org/2016/08/07/1608/076-bottom-dialog-fragment/)



#### 有标签的文本控件

[TagEditText](https://limedroid.github.io/2016/11/19/TagEditText/)



#### 灵活布局

[flexbox-layout](https://github.com/google/flexbox-layout)



### 传输

#### FlatBuffer

[数据交换格式FlatBuffers介绍](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0831/3395.html)

#### 后台服务下载网络数据

[在service里开线程用Hander来传递信息](http://www.open-open.com/code/view/1430626559031)



### 数据验证

#### 正则

[检查邮箱名、电话号码、用户密码、邮政编码](http://www.open-open.com/code/view/1428562396385)



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



### 缓存

#### SharedPreferences

```java
public class PreferenceUtils {

    private static final String PREFERENCE_FILE_NAME = "config";
    private SharedPreferences sharedPreferences;

    private SharedPreferences.Editor shareEditor;

    private static volatile PreferenceUtils preferenceUtils = null;


    protected PreferenceUtils(Context context) {
//        sharedPreferences = context.getSharedPreferences(PREFERENCE_FILE_NAME, Context.MODE_PRIVATE);

        sharedPreferences = PreferenceManager.getDefaultSharedPreferences(context);

        shareEditor = sharedPreferences.edit();
    }

    public static PreferenceUtils getInstance(Context context) {
        if (preferenceUtils == null) {
            synchronized (PreferenceUtils.class) {
                if (preferenceUtils == null) {
                    preferenceUtils = new PreferenceUtils(context.getApplicationContext());
                }
            }
        }
        return preferenceUtils;
    }

    public String getStringParam(String key) {
        return getStringParam(key, "");
    }

    public String getStringParam(String key, String defaultString) {
        return sharedPreferences.getString(key, defaultString);
    }

    public void saveParam(String key, String value) {
        shareEditor.putString(key, value).apply();
    }

    public boolean getBooleanParam(String key) {
        return getBooleanParam(key, false);
    }

    public boolean getBooleanParam(String key, boolean defaultBool) {
        return sharedPreferences.getBoolean(key, defaultBool);
    }

    public void saveParam(String key, boolean value) {
        shareEditor.putBoolean(key, value).apply();
    }

    public int getIntParam(String key) {
        return getIntParam(key, 0);
    }

    public int getIntParam(String key, int defaultInt) {
        return sharedPreferences.getInt(key, defaultInt);
    }

    public void saveParam(String key, int value) {
        shareEditor.putInt(key, value).apply();
    }

    public long getLongParam(String key) {
        return getLongParam(key, 0);
    }

    public long getLongParam(String key, long defaultInt) {
        return sharedPreferences.getLong(key, defaultInt);
    }

    public void saveParam(String key, long value) {
        shareEditor.putLong(key, value).apply();
    }

    public void removeKey(String key) {
        shareEditor.remove(key).apply();
    }
}
```

[SharedPreferences封装类SPUtils](http://www.open-open.com/code/view/1421140395968)

#### 清除缓存

[Android清除本地数据缓存代码](http://www.open-open.com/code/view/1450186362672)



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

[Retrofit2文件上传下载及其进度显示](http://ittiger.cn/Retrofit2%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0%E4%B8%8B%E8%BD%BD%E5%8F%8A%E5%85%B6%E8%BF%9B%E5%BA%A6%E6%98%BE%E7%A4%BA.html)



### 账号验证

#### AccountManager

[android账号创建，管理，同步](http://www.jianshu.com/p/c9337be547ae)



### 注解

#### Dagger2

[Dagger2 使用详解](http://www.jianshu.com/p/94d47da32656)



### 即时通讯

[源码提供！Android即时通讯和sns开源项目汇总](http://www.jianshu.com/p/b2ca52337fe5)

[练习环信即时通讯项目](https://github.com/jiangzehui/HX)



### 视频播放

[TigerVideo](https://github.com/huyongli/TigerVideo)

[Retrotfit2.1+Material Design+ijkplayer APP](https://github.com/jiangzehui/MD)



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



#### 截屏

[使用grade的命令行做gif](http://blog.csdn.net/a153614131/article/details/54137734)



### 错误锦集

[Android Studio出现Error:No service of type Factory available in ProjectScopeServices](http://www.jianshu.com/p/c4f4894ad215)

[Error:Cause: com.android.sdklib.repository.FullRevision](http://blog.csdn.net/caiwenfeng_for_23/article/details/51167143)



### Demo效果

#### Demo集合

[泡在网上的日子demo收集大全](http://www.jcodecraeer.com/plus/list.php?tid=31&codecategory=22000)

[泡在网上的日子demo收集大全2](http://www.jcodecraeer.com/plus/list.php?tid=31&TotalResult=1217&PageNo=1)

[Android全能网站](http://android.ctolib.com/)



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




#### [GeekNews](https://github.com/codeestX/GeekNews)

> A pure reading App based on Material Design + MVP + RxJava + Retrofit + Dagger2 + Realm + Glide

采用的技术：

- 使用RxJava配合Retrofit2做网络请求
- 使用RxUtil对线程操作和网络请求结果处理做了封装
- 使用RxPresenter对订阅的生命周期做管理
- 使用RxBus来方便组件间的通信
- 使用RxJava其他操作符来做延时、轮询、转化、筛选等操作
- 使用okhttp3对网络返回内容做缓存，还有日志、超时重连、头部消息的配置
- 使用Material Design控件和动画
- 使用MVP架构整个项目，对应于model、ui、presenter三个包
- 使用Realm做阅读记录和收藏记录的增、删、查、改
- 使用Glide做图片的处理和加载
- 使用Fragmentation简化Fragment的操作和懒加载
- 使用RecyclerView实现下拉刷新、上拉加载、侧滑删除、长按拖曳
- 使用x5WebView做阅览页，比原生WebView体验更佳
- 使用SVG及其动画实现progressbar的效果
- 使用EasyPermissions做6.0+动态权限适配
- 使用原生的夜间模式、分享、反馈
- 包含搜索、收藏、检测更新等功能
- 开启页的展示
- 选择日期的功能
- 向上滑动，底部栏会出现，向下滑动，底部栏会消失
- 直接复制到粘贴板




#### [StylishMusicPlayer](https://github.com/ryanhoo/StylishMusicPlayer)

> A stylish music player for android device 16+

采用的技术：

- RxJava
- RxAndroid
- Retrofit
- Butter Knife
- Calligraphy
- LiteOrm




#### [CloudReader](https://github.com/youlookwhat/CloudReader)

> 一个仿网易云音乐UI，使用Gank.Io及豆瓣Api开发的开源项目

采用的技术：

- 干货集中营内容与豆瓣电影书籍内容。
- 高仿网易云音乐歌单详情页。
- NavigationView搭配DrawerLayout的具体使用。
- MvvM-DataBing的项目应用。
- RxBus代替EventBus进行组件之间通讯。
- ToolBar及TabLayout的使用姿势。
- Glide加载监听，获取缓存，圆角图片，高斯模糊。
- 水波纹点击效果详细使用与适配。
- RecyclerView下拉刷新上拉加载。
- 基于DataBinding的ViewHolder。
- 基于DataBinding的BaseActivity和BaseFragment。
- Fragment懒加载模式。
- 沉浸式状态栏使用与版本适配。
- SwipeRefreshLayout结合RecyclerView下拉刷新上拉加载。
- CoordinatorLayout + Behavior实现标题栏渐变。
- NestedScrollView嵌套RecyclerView的使用。




#### [GanHuoIO](https://github.com/burgessjp/GanHuoIO)

> 基于Gank.IO提供的API的第三方客户端（RxJava+Retrofit）

主要特色：

- 基于 Material Design，项目中覆盖了 MVP、RxJava、Retrofit、第三方登录以及很多第三方库的使用。
- App可以即时的检查最新版本，还支持下载
- 有底部浏览bar




#### [bilibili-android-client](https://github.com/HotBitmapGG/bilibili-android-client)

> 高仿高仿哔哩哔哩动画安卓客户端

采用技术：

- [RxJava](https://github.com/ReactiveX/RxJava)
- [RxAndroid](https://github.com/ReactiveX/RxAndroid)
- [RxBinding](https://github.com/JakeWharton/RxBinding)
- [RxLifecycle](https://github.com/trello/RxLifecycle)
- [RxCache](https://github.com/VictorAlbertos/RxCache)
- [okhttp](https://github.com/square/okhttp)
- [retrofit](https://github.com/square/retrofit)
- [ijkplayer](https://github.com/Bilibili/ijkplayer)
- [DanmakuFlameMaster](https://github.com/Bilibili/DanmakuFlameMaster)
- [butterknife](https://github.com/JakeWharton/butterknife)
- [glide](https://github.com/bumptech/glide)
- [MaterialSearchView](https://github.com/MiguelCatalan/MaterialSearchView)
- [FlycoTabLayout](https://github.com/H07000223/FlycoTabLayout)
- [MagicaSakura](https://github.com/Bilibili/MagicaSakura)
- [FlowLayout](https://github.com/hongyangAndroid/FlowLayout)




[阅读视频类APP-MD](https://github.com/jiangzehui/MD)

采用的技术：

Retrotfit2.1+Material Design+ijkplayer 




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



[CaptchaImageView](https://github.com/jineshfrancs/CaptchaImageView)

> 自定义验证码



[GSYVideoPlayer](https://github.com/CarGuo/GSYVideoPlayer)

> 视频播放器（IJKplayer），支持基本的拖动，声音、亮度调节，支持边播边缓存，支持视频本身自带rotation的旋转（90,270之类），重力旋转与手动旋转的同步支持，支持列表播放 ，直接添加控件为封面，列表全屏动画，视频加载速度，列表小窗口支持拖动，5.0的过场效果，调整比例，多分辨率切换，支持切换播放器，其他一些小动画效果。



[ijkplayer](https://github.com/Bilibili/ijkplayer)

> Bilibili出的视频播放器



[ExpandableTextView](https://github.com/Chen-Sir/ExpandableTextView)

> 可以展开的TextView



[GaussianBlur](https://github.com/jrvansuita/GaussianBlur)

> 高斯模糊



[Android路由框架设计与实现](http://www.sixwolf.net/blog/2016/03/23/Android%E8%B7%AF%E7%94%B1%E6%A1%86%E6%9E%B6%E8%AE%BE%E8%AE%A1/)

> 像在Web开放中一样使用一个url来打开一个Activity



[RxDownload](https://github.com/ssseasonnn/RxDownload)

> 基于RxJava和Retrofit打造的下载工具, 支持多线程下载和断点续传, 智能判断是否支持断点续传等功能



[SwipeCaptcha](https://github.com/mcxtzhang/SwipeCaptcha)

> Android 平台的滑动验证码



[ZXingGenerator](https://github.com/vivian8725118/ZXingGenerator)

> 花式二维码生成，提供了6种样式



[TriStateToggleButton](https://github.com/BeppiMenozzi/TriStateToggleButton)

> 三种状态的按钮



[ShareUtil](https://github.com/shaohui10086/ShareUtil)

> 社会化登录分享工具库



[AdvancedLuban](https://github.com/shaohui10086/AdvancedLuban)

> 高效、简洁的图片压缩工具库



[Luban](https://github.com/Curzibn/Luban)

> 可能是最接近微信朋友圈的图片压缩算法



[loadtoast](https://github.com/code-mc/loadtoast)

> 请求信息反馈动画框



[HollyViewPager](https://github.com/florent37/HollyViewPager)

> 有预览的viewpager



[CircleProgress](https://github.com/lzyzsd/CircleProgress)

> 圆形进度条



[FABProgressCircle](https://github.com/JorgeCastilloPrz/FABProgressCircle)

> 带有FAB的进度圈



[Android-Week-View](https://github.com/alamkanak/Android-Week-View)

> 一周的计划日历



[MPAndroidChart](https://github.com/PhilJay/MPAndroidChart)

> 一款强大的图表



[ShineButton](https://github.com/ChadCSong/ShineButton)

> 有动画的花式点赞和收藏



[android-floating-action-button](https://github.com/futuresimple/android-floating-action-button)

> 会弹出来的FAB



[material-sheet-fab](https://github.com/gowong/material-sheet-fab)

> 通过点击FAB出来的菜单



[bottomsheet](https://github.com/Flipboard/bottomsheet)

> 出一半的底部菜单



[android-process-button](https://github.com/dmytrodanylyk/android-process-button)

> 可以显示加载进度的按钮



[circular-progress-button](https://github.com/dmytrodanylyk/circular-progress-button)

> 可以显示加载进度的圆形按钮



[RecyclerViewSwipeDismiss](https://github.com/CodeFalling/RecyclerViewSwipeDismiss)

> 可以拖动删除的RecyclerView



[AndroidTreeView](https://github.com/bmelnychuk/AndroidTreeView)

> 目录树



[excelPanel](https://github.com/zhouchaoyuan/excelPanel)

> 课表类似的excel界面



[MarqueeViewLibrary](https://github.com/gongwen/MarqueeViewLibrary)

> 跑马灯类似的移动公告



[CounterFab](https://github.com/andremion/CounterFab)

> 可以在FAB上显示消息数量



[ValidationUtilsLibrary](https://github.com/sgaikar1/ValidationUtilsLibrary)

>可以显示提示的EditText



[AnimShopButton](https://github.com/mcxtzhang/AnimShopButton)

> 一个带伸缩位移旋转动画的购物车按钮



[RxFingerPrinter](https://github.com/Zweihui/RxFingerPrinter)

> 用rxjava简单封装了指纹识别，顺便撸了一个指纹控件



[TopRightMenu](https://github.com/zaaach/TopRightMenu)

> 类似手机QQ界面右上角的弹出菜单



[material-about-library](https://github.com/daniel-stoneuk/material-about-library)

> material风格的关于页面



[ImagePicker](https://github.com/martin90s/ImagePicker)

> 功能超强的图片选择器



[Toasty](https://github.com/GrenderG/Toasty)

> 带有图片的toast



[RecyclerStickyHeaderView](https://github.com/TellH/RecyclerStickyHeaderView)

> 吸顶RecyclerView



[StickyHeaderListView](https://github.com/smuyyh/StickyHeaderListView)

> 仿滴滴打车开具发票页，ListView粘性Header



[TimerView](https://github.com/fashare2015/TimerView)

> 一个解耦良好的计时控件，可自由扩展。



[EdgeTranslucent](https://github.com/qinci/EdgeTranslucent)

> Android 任意View边沿渐变透明



[BottomMenuTutorial](https://github.com/fccaikai/BottomMenuTutorial)

> 底部menu弹出,抽屉控件



[plaid](https://github.com/nickbutcher/plaid)

> 上划退出



[ShareElementDemo](https://github.com/fashare2015/ShareElementDemo)

> 下拉回退和过场动画两个效果



[BottomNavigationViewEx](https://github.com/ittianyu/BottomNavigationViewEx)

> 一个增强BottomNavigationView的安卓库



[PictureSelector](https://github.com/LuckSiege/PictureSelector)

> 兼容性超强的图片选择器



[LinkedScrollDemo](https://github.com/fashare2015/LinkedScrollDemo)

> 一个仿饿了么订餐页面的双列表联动Demo



[ByeBurger](https://github.com/githubwing/ByeBurger)

> 极其简便的快速实现滑动隐藏标题栏和导航栏



[TaoBaoUI](https://github.com/gnehsuy/TaoBaoUI)

> 自己写的高仿淘宝界面



[AndroidViewAnimations](https://github.com/daimajia/AndroidViewAnimations)

> 安卓的类似PPT动画



[Router](https://github.com/daimajia/Router)

> 代码家做的安卓路由





### 代码开源协议

[程序员需要了解的版权协议](https://github.com/GcsSloop/AndroidNote/blob/magic-world/ChaosCrystal/%E5%BC%80%E6%BA%90%E5%85%B1%E4%BA%AB%E5%8D%8F%E8%AE%AE.md)



### 安卓笔记

[AndroidNote](https://github.com/GcsSloop/AndroidNote)

[Android开发总结](https://github.com/JohnTsaiAndroid/AndroidTips)
