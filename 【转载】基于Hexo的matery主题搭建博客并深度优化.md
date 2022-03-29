---
title: 【转载】基于Hexo的matery主题搭建博客并深度优化
date: 2021-12-11 22:20:47
mathjax: false
summary: 
categories: 
  - blog

tags:
  - hexo
---
## 基于Hexo的matery主题搭建博客并深度优化

[悟尘80](https://www.jianshu.com/u/738be5d6545a)

对于有一定技术背景的同学，自己动手搭建博客网站是一个很不错的选择。选择喜欢的主题，按需进行个性化配置，随时在本地用自己喜欢的工具写文章，一键发布到多个博客托管平台，使用自己喜欢的图床/CDN来加速...

> [演示站点（悟尘记）](https://links.jianshu.com/go?to=http%3A%2F%2Flixl.cn) 基于 Hexo 的 hexo-theme-matery 主题构建，部署在腾讯云COS中并使用CDN进行内容加速，通过 PicGo + 阿里云OSS 作为图床进行静态资源加速。

## 安装hexo

[Hexo](https://hexo.io/zh-cn/) 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

### 前提

安装 Hexo 相当简单，只需要先安装下列应用程序即可：

- [Node.js](http://nodejs.org/) (Node.js 版本需不低于 8.10，建议使用 Node.js 10.0 及以上版本)
- [Git](http://git-scm.com/)

### 安装

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。



```bash
$ npm install -g hexo-cli
```

安装以后，可以使用以下两种方式执行 Hexo：

1. `npx hexo`

2. 将 Hexo 所在的目录下的 `node_modules` 添加到环境变量之中即可直接使用 `hexo`：

   

   ```bash
   echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
   ```

### 建站

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。



```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

新建完成后，指定文件夹的目录如下：



```bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

### 启动

此时，通过 `hexo s` 命令即可在本地启动您的博客站点了。



```bash
~ hexo s
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```

接下来将安装主题，配置博客托管平台，实现一键发布并刷新CDN缓存。

## 配置主题

### 下载主题

[hexo-theme-matery](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fblinkfox%2Fhexo-theme-matery) 是一个采用 `Material Design` 和响应式设计的 Hexo 博客主题，点击 [这里](https://www.lixl.cn) 可以查看示例效果。点击 [这里](https://codeload.github.com/blinkfox/hexo-theme-matery/zip/master) 下载 `master` 分支的最新稳定版的代码，解压缩后，将 `hexo-theme-matery` 的文件夹复制到 Hexo 的 `themes` 文件夹中即可。

### 切换主题

修改 Hexo 根目录下的 `_config.yml` 的 `theme` 的值：`theme: hexo-theme-matery`

#### `_config.yml` 文件的其它修改建议:

- 请修改 `_config.yml` 的 `url` 的值为你的网站主 `URL`（如：`http://xxx.github.io`）。
- 建议修改两个 `per_page` 的分页条数值为 `6` 的倍数，如：`12`、`18` 等，这样文章列表在各个屏幕下都能较好的显示。
- 如果是中文用户，则建议修改 `language` 的值为 `zh-CN`。

### 新建分类 categories 页

`categories` 页是用来展示所有分类的页面，如果 `source` 目录下还没有 `categories/index.md` 文件，那么就需要新建一个，命令如下：



```bash
hexo new page "categories"
```

编辑你刚刚新建的页面文件 `/source/categories/index.md`，至少需要以下内容：



```yaml
---
title: categories
date: 2018-09-30 17:25:30
type: "categories"
layout: "categories"
---
```

### 新建标签 tags 页

`tags` 页是用来展示所有标签的页面，如果 `source` 目录下还没有 `tags/index.md` 文件，那么就需要新建一个，命令如下：



```bash
hexo new page "tags"
```

编辑刚刚新建的页面文件 `/source/tags/index.md`，至少需要以下内容：



```yaml
---
title: tags
date: 2018-09-30 18:23:38
type: "tags"
layout: "tags"
---
```

### 新建关于我 about 页

`about` 页是用来展示**关于我和我的博客**信息的页面，如果 `source` 目录下还没有 `about/index.md` 文件，那么就需要新建一个，命令如下：



```bash
hexo new page "about"
```

编辑刚刚新建的页面文件 `/source/about/index.md`，至少需要以下内容：



```yaml
---
title: about
date: 2018-09-30 17:25:30
type: "about"
layout: "about"
---
```

### 新建友情连接 friends 页（可选的）

`friends` 页是用来展示**友情连接**信息的页面，如果 `source` 目录下还没有 `friends/index.md` 文件，那么就需要新建一个，命令如下：



```bash
hexo new page "friends"
```

编辑刚刚新建的页面文件 `/source/friends/index.md`，至少需要以下内容：



```yaml
---
title: friends
date: 2018-12-12 21:25:30
type: "friends"
layout: "friends"
---
```

同时，在 `source` 目录下新建 `_data` 目录，在 `_data` 目录中新建 `friends.json` 文件，文件内容如下所示：



```json
[{
    "avatar": "https://www.lixl.cn/medias/avatar.jpg",
    "name": "悟尘记",
    "introduction": "人生就是一场修行，上善若水，厚德载物。",
    "url": "https://www.lixl.cn/",
    "title": "前去参观"
}, {
    "avatar": "https://wiki.hyperledger.org/download/attachments/2392069/fabric?version=1&modificationDate=1540928132000&api=v2",
    "name": "Fabric",
    "introduction": "A Blockchain Platform for the Enterprise",
    "url": "https://hyperledger-fabric.readthedocs.io/en/master/",
    "title": "前去学习"
}, {
    "avatar": "https://www.bootcdn.cn/assets/img/maoyun.svg",
    "name": "BootCDN",
    "introduction": "稳定、快速、免费的前端开源项目 CDN 加速服务。",
    "url": "https://www.bootcdn.cn/",
    "title": "前去加速"
}]
```

### 代码高亮

由于 Hexo 自带的代码高亮主题显示不好看，所以主题中使用到了 [hexo-prism-plugin](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fele828%2Fhexo-prism-plugin) 的 Hexo 插件来做代码高亮，安装命令如下：



```bash
npm i -S hexo-prism-plugin
```

然后，修改 Hexo 根目录下 `_config.yml` 文件中 `highlight.enable` 的值为 `false`，并新增 `prism` 插件相关的配置，主要配置如下：



```yaml
highlight:
  enable: false

prism_plugin:
  mode: 'preprocess'    # realtime/preprocess
  theme: 'tomorrow'
  line_number: false    # default false
  custom_css:
```

### 搜索

本主题中还使用到了 [hexo-generator-search](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fwzpan%2Fhexo-generator-search) 的 Hexo 插件来做内容搜索，安装命令如下：



```bash
npm install hexo-generator-search --save
```

在 Hexo 根目录下的 `_config.yml` 文件中，新增以下的配置项：



```yaml
search:
  path: search.xml
  field: post
```

### 修改页脚

页脚信息可能需要做定制化修改，而且它不便于做成配置信息，所以可能需要你自己去再修改和加工。修改的地方在主题文件的 `/layout/_partial/footer.ejs` 文件中，包括站点、使用的主题、访问量等。

### 修改社交链接

在主题的 `_config.yml` 文件中，默认支持 `QQ`、`GitHub` 和邮箱的配置，可以在主题文件的 `/layout/_partial/social-link.ejs` 文件中，新增、修改需要的社交链接地址，增加链接可参考如下代码：



```html
<a href="https://github.com/blinkfox" class="tooltipped" target="_blank" data-tooltip="访问我的GitHub" data-position="top" data-delay="50">
    <i class="fa fa-github"></i>
</a>
```

其中，社交图标（如：`fa-github`）可以在 [Font Awesome](https://fontawesome.com/icons) 中搜索找到。以下是常用社交图标的标识，供参考：

- Facebook: `fa-facebook`
- Twitter: `fa-twitter`
- Google-plus: `fa-google-plus`
- Linkedin: `fa-linkedin`
- Tumblr: `fa-tumblr`
- Medium: `fa-medium`
- Slack: `fa-slack`
- 新浪微博: `fa-weibo`
- 微信: `fa-wechat`
- QQ: `fa-qq`

### 修改打赏的二维码图片

在主题文件的 `source/medias/reward` 文件中，可以替换成你的的微信和支付宝的打赏二维码图片。

### 一键部署

通过 [hexo-deployer-git](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fhexojs%2Fhexo-deployer-git) 插件可以实现一键将博客同时部署到多个git仓库中。如同时发布到github及gitee提供的pages服务。安装：



```bash
npm install hexo-deployer-git --save
```

修改 Hexo 根目录下的 `_config.yml` 文件中的如下内容:



```yaml
## Docs: https://hexo.io/docs/deployment.html
deploy:
  - type: git
    repo: https://github.com/lxl80/blog.git
    branch: gh-pages
    ignore_hidden: false
  - type: git
    repo: https://gitee.com/lxl80/lxl80.git
    branch: master
    ignore_hidden: false
```

> 也可以如本站一样，采用 [hexo-deployer-cos-enhanced](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2F75k%2Fhexo-deployer-cos-enhanced) 插件将静态内容部署到腾讯云对象存储服务中，在DNS配置中将境内线路解析到腾讯云CDN地址，实现加速。部署完成后会自动刷新被更新文件的CDN缓存。

安装：



```bash
npm install hexo-deployer-cos-enhanced --save
```

`_config.yml` 配置如下:



```yaml
deploy:
  - type: git
    repo: https://github.com/lxl80/blog.git
    branch: gh-pages
    ignore_hidden: false
  - type: cos
    bucket: lxl80-130****
    region: ap-beijing
    secretId: AKIDh9****F8FvL
    secretKey: Z3IGiur****QZR3PgjXmlVg
    cdnConfig:
      enable: true
      cdnUrl: https://static.lixl.cn
      bucket: static-130****
      region: ap-beijing
      folder: static
      secretId: AKIDh9****F8FvL
      secretKey: Z3IGiur****QZR3PgjXmlVg
```

然后通过 `hexo g -d` 即可实现一键发布，并更新CDN缓存。

### 文章链接转静态短地址（建议安装）

如果文章名称是中文的，那么 Hexo 默认生成的永久链接也会有中文，这样不利于 `SEO`，且 `gitment` 评论对中文链接也不支持。我们可以用 [hexo-permalink-pinyin](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fviko16%2Fhexo-permalink-pinyin) Hexo 插件生成文章时生成中文拼音的永久链接，或者用[hexo-abbrlink](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Frozbo%2Fhexo-abbrlink) 生成静态文章链接。以下结合hexo-abbrlink生成类似 `/yyyy/mmdd+随机数.html` 的文章链接地址。

安装命令如下：



```bash
npm install hexo-abbrlink --save
```

在 Hexo 根目录下的 `_config.yml` 文件中，修改 `permalink:` ，并在文件末尾新增 `abbrlink:`配置项：



```yaml
permalink: :year/:month:day:abbrlink.html

abbrlink: 
  alg: crc16 #算法选项：crc16丨crc32
  rep: dec #输出进制：dec为十进制，hex为十六进制
```

### CND加速（建议启用）

放在Github的资源在国内加载速度比较慢，因此需要使用CDN加速来优化网站打开速度，[jsDelivr](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.jsdelivr.com%2F) + Github便是免费且好用的CDN，非常适合博客网站使用。也可以选择主流云服务商提供的对象存储+CDN来获得更快速及稳定的访问效果，费用低到几乎可忽略。

**用法：**



```http
https://cdn.jsdelivr.net/gh/你的用户名/你的仓库名@发布的版本号/文件路径
```

**例如：**



```http
https://cdn.jsdelivr.net/gh/lxl80/blog@gh-pages/medias/banner/1.jpg
```

注意：版本号不是必需的，是为了区分新旧资源，如果不使用版本号，将会直接引用最新资源。

> 还可以配合 [PicGo](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FMolunerfinn%2FPicGo)图床上传工具的**自定义域名前缀**来上传图片，使用极其方便。具体使用方法可参见我的另一篇文章: [使用Typora+iPic/PicGo图床+CDN实现高效Markdown创作](https://www.jianshu.com/2019/120114500.html)

### 文章字数统计插件（可选的）

如果你想要在文章中显示文章字数、阅读时长信息，可以安装 [hexo-wordcount](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fwillin%2Fhexo-wordcount)插件。

安装命令如下：



```bash
npm i --save hexo-wordcount
```

然后只需在本主题下的 `_config.yml` 文件中，激活以下配置项即可：



```yaml
wordCount:
  enable: false # 将这个值设置为 true 即可.
  postWordCount: true
  min2read: true
  totalCount: true
```

### 添加 RSS 订阅支持（可选的）

本主题中还使用到了 [hexo-generator-feed](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fhexojs%2Fhexo-generator-feed) 的 Hexo 插件来做 `RSS`，安装命令如下：



```bash
npm install hexo-generator-feed --save
```

在 Hexo 根目录下的 `_config.yml` 文件中，新增以下的配置项：



```yaml
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ' '
  order_by: -date
```

执行 `hexo clean && hexo g` 重新生成博客文件，然后在 `public` 文件夹中即可看到 `atom.xml` 文件，说明已经安装成功了。

## 自定制修改

在本主题的 `_config.yml` 中可以修改部分自定义信息，有以下几个部分：

- 菜单
- 我的梦想
- 首页的音乐播放器和视频播放器配置
- 是否显示推荐文章名称和按钮配置
- `favicon` 和 `Logo`
- 个人信息
- TOC 目录
- 文章打赏信息
- 复制文章内容时追加版权信息
- MathJax
- 文章字数统计、阅读时长
- 点击页面的'爱心'效果
- 我的项目
- 我的技能
- 我的相册
- `Gitalk`、`Gitment`、`Valine` 和 `disqus` 评论配置
- [不蒜子统计](https://links.jianshu.com/go?to=http%3A%2F%2Fbusuanzi.ibruce.info%2F)和谷歌分析（`Google Analytics`）
- 默认特色图的集合。当文章没有设置特色图时，本主题会根据文章标题的 `hashcode` 值取余，来选择展示对应的特色图

如果本主题中的诸多功能和主题色彩你不满意，可以在主题中自定义修改，很多更自由的功能和细节点的修改难以在主题的 `_config.yml` 中完成，需要修改源代码才来完成。以下列出了可能有用的地方：

### 修改主题颜色

在主题文件的 `/source/css/matery.css` 文件中，搜索 `.bg-color` 来修改背景颜色：



```css
/* 整体背景颜色，包括导航、移动端的导航、页尾、标签页等的背景颜色. */
.bg-color {
    background-image: linear-gradient(to right, #4cbf30 0%, #0f9d58 100%);
}

@-webkit-keyframes rainbow {
   /* 动态切换背景颜色. */
}

@keyframes rainbow {
    /* 动态切换背景颜色. */
}
```

### 修改 banner 图和文章特色图

可以直接在 `/source/medias/banner` 文件夹中更换喜欢的 `banner` 图片，主题代码中是每天动态切换一张，只需 `7` 张即可。如果会 `JavaScript` 代码，可以修改成自己喜欢切换逻辑，如：随机切换等，`banner` 切换的代码位置在 `/layout/_partial/bg-cover-content.ejs` 文件的 `<script></script>` 代码中：



```javascript
$('.bg-cover').css('background-image', 'url(/medias/banner/' + new Date().getDay() + '.jpg)');
```

在 `/source/medias/featureimages` 文件夹中默认有 24 张特色图片，你可以再增加或者减少，并需要在 `_config.yml` 做同步修改。

## 文章 Front-matter 介绍

### Front-matter 选项详解

`Front-matter` 选项中的所有内容均为**非必填**的。但仍然建议至少填写 `title` 和 `date` 的值。

| 配置选项   | 默认值                         | 描述                                                         |
| ---------- | ------------------------------ | ------------------------------------------------------------ |
| title      | `Markdown` 的文件标题          | 文章标题，强烈建议填写此选项                                 |
| date       | 文件创建时的日期时间           | 发布时间，强烈建议填写此选项，且最好保证全局唯一             |
| author     | 根 `_config.yml` 中的 `author` | 文章作者                                                     |
| img        | `featureImages` 中的某个值     | 文章特征图                                                   |
| top        | `true`                         | 推荐文章（文章是否置顶），如果 `top` 值为 `true`，则会作为首页推荐文章 |
| cover      | `false`                        | 表示该文章是否需要加入到首页轮播封面中                       |
| coverImg   | 无                             | 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片 |
| password   | 无                             | 文章阅读密码，如果要对文章设置阅读验证密码的话，就可以设置 `password` 的值，该值必须是用 `SHA256` 加密后的密码，防止被他人识破。前提是在主题的 `config.yml` 中激活了 `verifyPassword` 选项 |
| toc        | `true`                         | 是否开启 TOC，可以针对某篇文章单独关闭 TOC 的功能。前提是在主题的 `config.yml` 中激活了 `toc` 选项 |
| mathjax    | `false`                        | 是否开启数学公式支持 ，本文章是否开启 `mathjax`，且需要在主题的 `_config.yml` 文件中也需要开启才行 |
| summary    | 无                             | 文章摘要，自定义的文章摘要内容，如果这个属性有值，文章卡片摘要就显示这段文字，否则程序会自动截取文章的部分内容作为摘要 |
| categories | 无                             | 文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类 |
| tags       | 无                             | 文章标签，一篇文章可以多个标签                               |

> **注意**:
>
> 1. 如果 `img` 属性不填写的话，文章特色图会根据文章标题的 `hashcode` 的值取余，然后选取主题中对应的特色图片，从而达到让所有文章都的特色图**各有特色**。
> 2. `date` 的值尽量保证每篇文章是唯一的，因为本主题中 `Gitalk` 和 `Gitment` 识别 `id` 是通过 `date` 的值来作为唯一标识的。
> 3. 如果要对文章设置阅读验证密码的功能，不仅要在 Front-matter 中设置采用了 SHA256 加密的 password 的值，还需要在主题的 `_config.yml` 中激活了配置。有些在线的 SHA256 加密的地址，可供使用：[开源中国在线工具](https://links.jianshu.com/go?to=http%3A%2F%2Ftool.oschina.net%2Fencrypt%3Ftype%3D2)、[chahuo](https://links.jianshu.com/go?to=http%3A%2F%2Fencode.chahuo.com%2F)、[站长工具](https://links.jianshu.com/go?to=http%3A%2F%2Ftool.chinaz.com%2Ftools%2Fhash.aspx)。

以下为文章的 `Front-matter` 示例。

### 最简示例



```yaml
---
title: 基于Hexo的hexo-theme-matery主题搭建博客并优化
date: 2019-10-03 14:25:00
---
```

### 最全示例



```yaml
---
title: 基于Hexo的hexo-theme-matery主题搭建博客并优化
date: 2019-10-03 14:25:00
author: 悟尘
img: /source/images/xxx.jpg
top: true
cover: true
coverImg: /images/1.jpg
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: false
mathjax: false
summary: 这是你自定义的文章摘要内容，如果这个属性有值，文章卡片摘要就显示这段文字，否则程序会自动截取文章的部分内容作为摘要
categories: 工具
tags:
  - blog
  - hexo
---
```

## SEO优化

搜索引擎优化，又称为SEO，即Search Engine Optimization，它是一种通过分析搜索引擎的排名规律，了解各种搜索引擎怎样进行搜索、怎样抓取互联网页面、怎样确定特定关键词的搜索结果排名的技术。Google自动收录效果还不错，百度就差得远了（`GitHub`不允许百度的`Spider`爬取`GitHub`上的内容）。

### 百度优化

登录[百度搜索资源平台](https://links.jianshu.com/go?to=https%3A%2F%2Fziyuan.baidu.com%2F)， 登录成功之后在 用户中心 --> 站点管理 页面中点击[添加网站](https://links.jianshu.com/go?to=https%3A%2F%2Fziyuan.baidu.com%2Fsite%2Fsiteadd)，按提示操作。



![img](https://upload-images.jianshu.io/upload_images/10845339-9a905267913cf447.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)



> 提示：由于百度的spider是爬取不到GitHub的内容的，所以在第三步验证网站的时候，建议选择`CNAME验证`的方式。

经过以上步骤，百度已经知道有我们网站的存在了，但是百度还不知道我们的网站上有什么内容，所以要向百度推送我们的内容。`hexo-theme-matery`主题已经内置了 `自动推送` 的方式， 检查 `themes/hexo-theme-matery/_config.yml` 文件中如下配置:



```yaml
# 百度搜索资源平台提交链接
baiduPush: true
```

自动推送的JS代码部署在站点的每一个页面源代码中，当页面在每次被浏览时，链接就会被自动推送给百度。

### 谷歌优化

登录 [Google Search Console](https://links.jianshu.com/go?to=https%3A%2F%2Fsearch.google.com%2Fsearch-console%3Fhl%3Dzh-CN)，点击添加资源，输入自己的域名，按提示操作。

![谷歌优化](https://gitee.com/mr_tolie/pics/raw/master/images/202203271608320.png)

> 提示：需要进行DNS验证，进入DNS域名解析设置页面，按提示增加TXT记录，如下图:
>
> ![img](https://upload-images.jianshu.io/upload_images/10845339-a24a9f2a55cc1ffd.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

验证成功后，需要提交站点地图。通过安装sitemap插件生成站点地图文件:



```bash
npm install hexo-generator-sitemap --save 
npm install hexo-generator-baidu-sitemap --save  #百度专用，可选
```

安装后直接执行 `hexo cl&&hexo g -d` 命令，就会在网站根目录生成 `sitemap.xml` 文件。参照下图提交，等待收录。

![img](https://upload-images.jianshu.io/upload_images/10845339-93d3fb9db5647478.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)



> 注意：hexo配置文件中的url一定要输入正确的域名，插件是根据url生成站点地图的。

## 常用命令

### 指令说明

`hexo server` #启动本地服务器，用于预览主题。Hexo 会监视文件变动并自动更新，除修改站点配置文件外,无须重启服务器,直接刷新网页即可生效。

`hexo server -s` #以静态模式启动

`hexo server -p 5000` #更改访问端口 (默认端口为4000，'ctrl + c'关闭server)

`hexo server -i IP地址` #自定义 IP

`hexo clean` #清除缓存 ,网页正常情况下可以忽略此条命令,执行该指令后,会删掉站点根目录下的public文件夹

`hexo g` #生成静态网页 (执行 $ `hexo g`后会在站点根目录下生成public文件夹, hexo会将"/blog/source/" 下面的.md后缀的文件编译为.html后缀的文件,存放在"/blog/public/ " 路径下)

`hexo d` #自动生成网站静态文件，并将本地数据部署到设定的仓库(如github)

`hexo init` 文件夹名称 #初始化XX文件夹名称

`npm update hexo -g`#升级

`npm install hexo -g` #安装

`node-v` #查看node.js版本号

`npm -v` #查看npm版本号

`git --version` #查看git版本号

`hexo -v` #查看hexo版本号

### 简写指令

```
hexo n "我的第一篇文章"` 等价于 `hexo new "我的第一篇文章"` 还等价于 `hexo new post "我的第一篇文章"
hexo p` 等价于 `hexo publish
hexo g` 等价于 `hexo generate
hexo s`等价于 `hexo server
hexo d` 等价于 `hexo deploy
hexo g -d`等价于`hexo generate --deploy
```

注: `hexo clean` 没有 简写, `git --version` 没有简写

## 常见问题

1. **通过`hexo g -d`部署时报`Error: Spawn failed`错误:**

> 这是由于git本地记录的提交版本号与github上不一致导致的，通过`git reset --hard commitCode`即可解决。

- 检查本地最近提交记录，获取最后一次提交记录的更新时间及标识，如

  ```
  280a7fdd46fcfd7d34e652aec15523dcd247fac8
  ```

  

  ```bash
  cd .deploy_git
  cat .git/logs/HEAD  
  ```

- 获取github pages服务所关联分支的最近一次提交记录，获取更新时间及标识。地址一般为：`https://github.com/用户名/仓库名/commits/分支名`，如`https://github.com/lxl80/blog/commits/gh-pages`

- 如果发现提交最新的提交时间/标识不一致，通过以下命令即可解决:

  

  ```bash
    git reset --hard f085038efdf79546c09641d37b2a2429c1ae8e60 #github上最新的提交标识
  ```

1.设置模板，blog根目录 `scaffolds/post.md`
加入categories,tags等，这样以后通过 `hexo new` 生成的模板就不用写这两个单词了。
当然，你也可以写入任何你每个文章中都会有的部分。

```
---
title: {{ title }}
date: {{ date }}
categories:
tags:
---yaml复制代码
```

## Linux平台下的技巧

### 快捷命令

其实就通过alias，触发一些命令的集合
在 `~/.bashrc` 文件中添加

```
alias hs='hexo clean && hexo g && hexo s'  #启动本地服务
alias hd='hexo clean && hexo g && hexo d'  #部署博客bash复制代码
```

甚至你也可以加入备份文章的命令，可以自由发挥。

### 博客备份（快捷命令升级版）

为了保证我们写的文章不丢失、快速迁移博客，都需要备份我们的blog。

1. 博客根目录，执行 `git init` 创建 git 仓库。

2. 在 github（或其他托管平台、自建远程仓库等） 创建仓库并和本地仓库建立联系。

3. 在`~/.bashrc`文件中添加

   ```
   alias hs='hexo clean && hexo g && hexo s'
   alias hd='hexo clean && hexo g && hexo d && git add . && git commit -m "update" && git push -f'bash复制代码
   ```

这样，我们在执行 `hd` 进行部署时，就一同将博客进行备份了

## 参照

- [hexo官方文档](https://links.jianshu.com/go?to=https%3A%2F%2Fhexo.io%2Fzh-cn%2Fdocs%2F)
- [闪烁之狐](https://links.jianshu.com/go?to=https%3A%2F%2Fblinkfox.github.io%2F2018%2F09%2F28%2Fqian-duan%2Fhexo-bo-ke-zhu-ti-zhi-hexo-theme-matery-de-jie-shao%2F)
- [hexo-theme-matery](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fblinkfox%2Fhexo-theme-matery%2Fblob%2Fdevelop%2FREADME_CN.md)
- [Hexo进阶之各种优化](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.sky03.cn%2Fposts%2F42790.html%23toc-heading-1)