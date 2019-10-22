[原文链接](https://www.cnblogs.com/Sanje3000/p/6953118.html)
#####1.异常描述：
pointer being freed was not allocated
*** set a breakpoint in malloc_error_break to debug
#####2.原因：
通过排除法，发现只要不监听wkwebview.scrollview的delegate,就不会异常；
想起scrollview是strong引用：
@property (nonatomic, readonly, strong) UIScrollView *scrollView;
#####3.解决方法：
将delegate设置为nil：
````
- (void) dealloc
{
    if(self.webView)
     {
          self.webView.scrollView.delegate=nil;
     }
}
````

