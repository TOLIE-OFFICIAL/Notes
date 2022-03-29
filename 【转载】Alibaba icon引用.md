---
title: 【转载】Alibaba字体图标的使用
date: 2022-01-17 18:39:55
summary: 
categories: 
  - Frond End

tags:
  - icon
---
# Alibaba字体图标的使用

### Web 端使用

用户在 iconfont.cn 可以下载，多种格式的 icon，平台也可将图标转换为字体，便于前端工程师自由调整与调用。

#### icon 单个使用

------

单个图标用户可以自行选择下载不同的格式使用，包括 png、ai、svg。



点击下载按钮，可以选择下载图标。

![https://img.alicdn.com/tps/TB1PoyDNpXXXXX8aXXXXXXXXXXX-1168-650.png](https://img.alicdn.com/tps/TB1PoyDNpXXXXX8aXXXXXXXXXXX-1168-650.png)

此种方式适合用在图标引用特别少，以后也不需要特别维护的场景。

- 比如设计师用来做demo原型。
- 前端临时做个活动页。
- 当然如果你只是为了下载图标做PPT,也是极好的。

不过如果是成体系的应用使用，建议用户把icon加入项目，然后使用下面三种推荐的方式。



#### unicode 引用

------

unicode是字体在网页端最原始的应用方式，特点是：

- 兼容性最好，支持ie6+，及所有现代浏览器。
- 支持按字体的方式去动态调整图标大小，颜色等等。
- 但是因为是字体，所以不支持多色。只能使用平台里单色的图标，就算项目里有多色图标也会自动去色。

> 注意：新版iconfont支持多色图标，这些多色图标在unicode模式下将不能使用，如果有需求建议使用symbol的引用方式

unicode使用步骤如下：

##### 第一步：拷贝项目下面生成的font-face

```js
@font-face {font-family: 'iconfont';
    src: url('iconfont.eot');
    src: url('iconfont.eot?#iefix') format('embedded-opentype'),
    url('iconfont.woff') format('woff'),
    url('iconfont.ttf') format('truetype'),
    url('iconfont.svg#iconfont') format('svg');
}
```

##### 第二步：定义使用iconfont的样式

```js
.iconfont{
    font-family:"iconfont" !important;
    font-size:16px;font-style:normal;
    -webkit-font-smoothing: antialiased;
    -webkit-text-stroke-width: 0.2px;
    -moz-osx-font-smoothing: grayscale;}
```

##### 第三步：挑选相应图标并获取字体编码，应用于页面

```js
<i class="iconfont">&#x33;</i>
```



#### font-class 引用

------

font-class是unicode使用方式的一种变种，主要是解决unicode书写不直观，语意不明确的问题。

与unicode使用方式相比，具有如下特点：

- 兼容性良好，支持ie8+，及所有现代浏览器。
- 相比于unicode语意明确，书写更直观。可以很容易分辨这个icon是什么。
- 因为使用class来定义图标，所以当要替换图标时，只需要修改class里面的unicode引用。
- 不过因为本质上还是使用的字体，所以多色图标还是不支持的。

使用步骤如下：

##### 第一步：拷贝项目下面生成的fontclass代码：

```js
//at.alicdn.com/t/font_8d5l8fzk5b87iudi.css
```

##### 第二步：挑选相应图标并获取类名，应用于页面：

```css
<i class="iconfont icon-xxx"></i>
```



#### symbol 引用

------

这是一种全新的使用方式，应该说这才是未来的主流，也是平台目前推荐的用法。相关介绍可以参考这篇[文章](https://www.iconfont.cn/help/detail?spm=a313x.7781069.1998910419.d8cf4382a&helptype=code) 这种用法其实是做了一个svg的集合，与上面两种相比具有如下特点：

- 支持多色图标了，不再受单色限制。
- 通过一些技巧，支持像字体那样，通过`font-size`,`color`来调整样式。
- 兼容性较差，支持 ie9+,及现代浏览器。
- 浏览器渲染svg的性能一般，还不如png。

使用步骤如下：

##### 第一步：拷贝项目下面生成的symbol代码：

```js
//at.alicdn.com/t/font_8d5l8fzk5b87iudi.js
```

##### 第二步：加入通用css代码（引入一次就行）：

```js
<style type="text/css">
    .icon {
       width: 1em; height: 1em;
       vertical-align: -0.15em;
       fill: currentColor;
       overflow: hidden;
    }
</style>
```

##### 第三步：挑选相应图标并获取类名，应用于页面：

```js
<svg class="icon" aria-hidden="true">
    <use xlink:href="#icon-xxx"></use>
</svg>
```

##### symbol 引用案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>JD产品模块</title>
  <script src="//at.alicdn.com/t/font_2986248_ilxp137m7aj.js"></script>
  <style>
    * {
      margin: 0;
      padding: 0;

    }

    .icon {
      width: 1em;
      height: 1em;
      vertical-align: -0.15em;
      fill: currentColor;
      overflow: hidden;
    }
  </style>
</head>

<body>
  <div class="box">
    <img src="img/220117.webp" alt="">
    <svg class="icon" aria-hidden="true">
      <use xlink:href="#icon-ziying"></use>
    </svg>
  </div>
</body>

</html>
```



### Android 使用

Android 可以直接使用单个 icon(svg、png)。也可以直接引入字体应用：

##### 第一步：从 iconfont 平台选择要使用到的图标，并下载至本地；复制字体文件到项目 assets 目录

![https://img.alicdn.com/tps/TB1z4QbNpXXXXX4XFXXXXXXXXXX-882-730.gif](https://img.alicdn.com/tps/TB1z4QbNpXXXXX4XFXXXXXXXXXX-882-730.gif)

##### 第二步：打开从 iconfont 平台下载下来的文件，并在目录中打开demo.html，找到图标相对应的 HTML 实体字符码；

![https://img.alicdn.com/tfscom/T1p8FvFu8jXXaCwpjX.png](https://img.alicdn.com/tfscom/T1p8FvFu8jXXaCwpjX.png)

##### 第三步：打开 res/values/strings.xml，添加 string 值；

```html
<string name="icons">&#x3605; &#x35ad; &#x35ae; &#x35af;</string>
```

##### 第四步：打开 activity_main.xml，添加 string 值到TextView：

```html
<TextView

    android:id="../../+id/like"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="../../string/icons" />
```

##### 第五步：为 TextView 指定文字：

```html
import android.graphics.Typeface;
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    Typeface iconfont = Typeface.createFromAsset(getAssets(), "iconfont/iconfont.ttf");
    TextView textview = (TextView)findViewById(R.id.like);
    textview.setTypeface(iconfont);
}
```

![https://img.alicdn.com/tfscom/T1OvFvFCRlXXaCwpjX.png](https://img.alicdn.com/tfscom/T1OvFvFCRlXXaCwpjX.png)

### iOS 使用

iOS 可以直接使用单个icon(svg,png)。也可以直接引入字体应用：

#### 第一步：将您从IconFont平台下载的字体文件(.ttf)添加到工程中；

打开Info.plist文件，增加一个新的Array类型的键，键名设置为UIAppFonts（Fonts provided by application），增加字体的文件名：“iconfont.ttf“

![https://img.alicdn.com/tfscom/T1R3VxFuRnXXaCwpjX.png](https://img.alicdn.com/tfscom/T1R3VxFuRnXXaCwpjX.png)

#### 第二步：使用IconFont字体:

```
UILabel * label = [[UILabel alloc] initWithFrame:self.view.bounds];
UIFont *iconfont = [UIFont fontWithName:@"uxIconFont" size: 34];
label.font = iconfont;
label.text = @"\U00003439 \U000035ad \U000035ae \U000035af \U000035eb \U000035ec";
[self.view addSubview: label];
```

这里有两个地方注意下：

- 创建 UIFont 使用的是字体名，而不是文件名；
- 文本值为 8 位的 Unicode 字符，我们可以打开 demo.html 查找每个图标所对应的 HTML 实体 Unicode 码，比如： "店" 对应的 HTML 实体 Unicode 码为：0x3439 转换后为：\U00003439 就是将 0x 替换为 \U 中间用 0 填补满长度为 8 个字符。