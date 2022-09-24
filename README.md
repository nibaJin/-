# 可视化圈选模块原理与实践

原理： app通过上传当前屏幕截图以及截图相关的所有元素至后台，前端通过上传的数据进行可视化展示，以及可视化绑定。
例子：
![企业微信20220712-173300.png](https://github.com/nibaJin/visualization-module/blob/main/img/tapd_30391015_1657618402_7.png?raw=true)
![企业微信20220711-181646.png](https://github.com/nibaJin/visualization-module/blob/main/img/tapd_30391015_1657534624_58.png?raw=true)

### `1.elementMd5`
> 元素id，用于前端布局。
### `2.left、top、width、height`
> 布局定位元素位置和大小
> 这里使用相对父view的布局方式。
> !!#ff0000 列表坐标!!需要通过contentOffset特殊转换。因为这里的坐标都是绝对与父view的坐标，然而列表是可以滑动的。
### `3.subviewsMd5`
> 子元素id数组[sub_elementMd5, ... ]
### `4.spmXpathMd5`
> 元素唯一标识 xpath的md5
> 平时业务埋点，就会改动到这个xpath，比如设置瀑布流、区分共用元素xpath、稳固xpath、自定义xpath等等。
### `5.exposureEnable`
元素能否曝光
### `6.clickable`
元素能否点击
![企业微信20220712-165944.png](https://github.com/nibaJin/visualization-module/blob/main/img/tapd_30391015_1657616431_86.png?raw=true)

##平时埋点，我们其实就是在处理这两个字段：spmXpathMd5、exposureEnable
``` 
// 业务埋点-本质改动的字段：
1. spmXpathMd5 - 修改xpath，比如设置瀑布流、区分共用元素xpath、稳固xpath、自定义xpath等等。
2. exposureEnable - 标记元素曝光。
```

**参谋后台展示：**
![企业微信20220711-182259.png](https://github.com/nibaJin/visualization-module/blob/main/img/tapd_30391015_1657535001_6.png?raw=true)
