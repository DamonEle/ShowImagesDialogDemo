# ShowImagesDialogDemo
PhotoView+Glide+Dialog+ViewPager:打造轻量级的图片浏览方案
其实不单单是做简单的图片浏览、android原生的dialog可以做到activity、fragment的大部分展示功能，而且更轻量化，易于封装与维护。

### 几点需要注意的地方
### 由于是PhotoView嵌套了Viewpager，滑动时有一定几率崩溃，github上已经给出了对应的解决方案：继承一个viewpager，在相关方法里try catch 异常。
```/**
 * 为了解决photoview嵌套在部分父控件时闪退的bug，github上提供的解决方案
 */
public class ShowImagesViewPager extends ViewPager {
    
    @Override
    public boolean onInterceptTouchEvent(MotionEvent ev) {
        try {
            return super.onInterceptTouchEvent(ev);
        } catch (IllegalArgumentException e) {
            //uncomment if you really want to see these errors
            //e.printStackTrace();
            return false;
        }
    }
}
```

### 为了使dialog具有全屏透明效果，需要给我们的dialog一个新的style。

```<!--全屏背景半透明 dialog-->
    <style name="transparentBgDialog" parent="@android:style/Theme.Dialog">
        <item name="android:windowFrame">@null</item>
        <item name="android:windowIsFloating">true</item>
        <item name="android:windowIsTranslucent">true</item>
        <item name="android:windowBackground">@color/transparent</item>
        <item name="android:backgroundDimEnabled">true</item>
        <item name="android:background">@color/transparent</item>
        <item name="android:windowNoTitle">true</item>
    </style>

```

### 所以，马上替换吧！

![dialog正常显示photoview](http://upload-images.jianshu.io/upload_images/3417659-e81582bfaf009d2a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/340)

*dialog正常显示photoview*

![同一张图片缩放后的photoview](http://upload-images.jianshu.io/upload_images/3417659-59c183019c7a0232.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/340)

*同一张图片缩放后的photoview*

![图片](http://upload-images.jianshu.io/upload_images/3417659-5daf8fdd69a8aa3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/340)
