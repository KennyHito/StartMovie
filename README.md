前言
----------------------
* 本工程主要是利用iOS 的Objective-C开发的技术要点汇总；
* 涵盖了开发中踩坑的原因，以及填坑的技术分享；
* 抛砖引玉，取长补短，希望能够提供一点思路，避免少走一些弯路。

要求
----------------

* iOS 8+
* Xcode 8.0+

期待
----------------

* 如果在使用过程中遇到BUG，希望你能[Issues](https://github.com/NSLog-YuHaitao/iOSReview/issues)我，谢谢(或者尝试下载最新的代码看看BUG修复没有)。
* 如果在使用过程中发现有更好或更巧妙的实用技术，希望你能[Issues](https://github.com/NSLog-YuHaitao/iOSReview/issues)我，我非常为该项目扩充更多好用的技术，谢谢。
* 如果通过该工程的使用，对您在开发中有一点帮助，码字不易，还请点击右上角star按钮，谢谢。


核心代码
----------------------

~~~
NSString *versionCache = [[NSUserDefaults standardUserDefaults] objectForKey:@"VersionCache"];//本地缓存的版本号  第一次启动的时候本地是没有缓存版本号的。
NSString *version = [[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBundleShortVersionString"];//当前应用版本号

if (![versionCache isEqualToString:version]){
//如果本地缓存的版本号和当前应用版本号不一样，则是第一次启动（更新版本也算第一次启动）
MovieViewController *wsCtrl = [[MovieViewController alloc]init];
wsCtrl.movieURL = [NSURL fileURLWithPath:[[NSBundle mainBundle]pathForResource:@"qidong"ofType:@"mp4"]];//选择本地的视屏
self.window.rootViewController = wsCtrl;

//设置上下面这句话，将当前版本缓存到本地，下次对比一样，就不走启动视屏了。
//也可以将这句话放在WSMovieController.m的进入应用方法里面
//为了让每次都可以看到启动视屏，这句话先注释掉
[[NSUserDefaults standardUserDefaults] setObject:version forKey:@"VersionCache"];

}else{
//不是首次启动
RootTabBarController *rootTabCtrl = [[RootTabBarController alloc]init];
self.window.rootViewController = rootTabCtrl;
}
~~~

效果图
------------------

![效果图](111.gif)
