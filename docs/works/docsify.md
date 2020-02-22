

# docsify简介

# [快速开始](https://docsify.js.org/#/quickstart?id=quick-start)

建议`docsify-cli`全局安装，这有助于在本地初始化和预览网站。

```bash
npm i docsify-cli -g
```

## [初始化](https://docsify.js.org/#/quickstart?id=initialize)

如果要在`./docs`子目录中编写文档，则可以使用`init`命令。

```bash
docsify init ./docs
```

## [写作内容](https://docsify.js.org/#/quickstart?id=writing-content)

在之后`init`完成后，你可以看到在文件列表`./docs`子目录。

- `index.html` 作为入口文件
- `README.md` 作为主页
- `.nojekyll` 防止GitHub Pages忽略以下划线开头的文件

您可以轻松地更新文档`./docs/README.md`，当然您可以添加[更多页面](https://docsify.js.org/#/more-pages)。

## [预览您的网站](https://docsify.js.org/#/quickstart?id=preview-your-site)

使用运行本地服务器`docsify serve`。您可以在上的浏览器中预览站点`http://localhost:3000`。

```bash
docsify serve docs
```

有关的更多用例`docsify-cli`，请转到[docsify-cli文档](https://github.com/docsifyjs/docsify-cli)。

## [手动初始化](https://docsify.js.org/#/quickstart?id=manual-initialization)

如果您不喜欢`npm`该工具或在安装该工具时遇到问题，可以手动创建`index.html`：

```html
<!-- index.html -->

<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta charset="UTF-8">
  <link rel="stylesheet" href="//unpkg.com/docsify/themes/vue.css">
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      //...
    }
  </script>
  <script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
</body>
</html>
```

如果您在系统上安装了python，则可以轻松地使用它运行静态服务器来预览站点。

```bash
cd docs && python -m SimpleHTTPServer 3000
```

## [载入对话框](https://docsify.js.org/#/quickstart?id=loading-dialog)

如果需要，您可以在docsify开始呈现文档之前显示一个加载对话框：

```html
  <!-- index.html -->

  <div id="app">Please wait...</div>
```

`data-app`如果更改，则应设置属性`el`：

```html
  <!-- index.html -->

  <div data-app id="main">Please wait...</div>

  <script>
    window.$docsify = {
      el: '#main'
    }
  </script>
```



如果需要更多页面，只需在docsify目录中创建更多markdown文件即可。如果创建一个名为的文件`guide.md`，则可以通过访问该文件`/#/guide`。

例如，目录结构如下：

```text
.
└── docs
    ├── README.md
    ├── guide.md
    └── zh-cn
        ├── README.md
        └── guide.md
```

匹配路线

```text
docs/README.md        => http://domain.com
docs/guide.md         => http://domain.com/#/guide
docs/zh-cn/README.md  => http://domain.com/#/zh-cn/
docs/zh-cn/guide.md   => http://domain.com/#/zh-cn/guide
```

## [侧边栏](https://docsify.js.org/#/more-pages?id=sidebar)

为了拥有侧边栏，您可以创建自己[的侧边栏（](https://github.com/docsifyjs/docsify/blob/master/docs/_sidebar.md)有关示例，`_sidebar.md`请参见[本文档的侧边栏](https://github.com/docsifyjs/docsify/blob/master/docs/_sidebar.md)）：

首先，您需要设置`loadSidebar`为**true**。有关详细信息，请参见[配置段落](https://docsify.js.org/#/configuration?id=loadsidebar)。

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true
  }
</script>
<script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
```

创建`_sidebar.md`：

```markdown
<!-- docs/_sidebar.md -->

* [Home](/)
* [Guide](guide.md)
```

您需要创建一个`.nojekyll`in `./docs`来防止GitHub Pages忽略以下划线开头的文件。

## [嵌套侧边栏](https://docsify.js.org/#/more-pages?id=nested-sidebars)

您可能希望边栏仅通过导航进行更新以反映当前目录。可以通过将`_sidebar.md`文件添加到每个文件夹来完成。

`_sidebar.md`从每个级别目录加载。如果当前目录没有`_sidebar.md`，它将退回到上级目录。例如，如果当前路径为`/guide/quick-start`，`_sidebar.md`则将从中加载`/guide/_sidebar.md`。

您可以指定`alias`以避免不必要的回退。

```html
<script>
  window.$docsify = {
    loadSidebar: true,
    alias: {
      '/.*/_sidebar.md': '/_sidebar.md'
    }
  }
</script>
```

您可以`README.md`在子目录中创建文件，以将其用作路线的登录页面。

## [从侧边栏选择设置页面标题](https://docsify.js.org/#/more-pages?id=set-page-titles-from-sidebar-selection)

页面的`title`标签是根据*所选的*侧边栏项目名称生成的。为了获得更好的SEO，您可以通过在文件名后指定字符串来自定义标题。

```markdown
<!-- docs/_sidebar.md -->
* [Home](/)
* [Guide](guide.md "The greatest guide in the world")
```

## [目录](https://docsify.js.org/#/more-pages?id=table-of-contents)

创建完成后`_sidebar.md`，边栏内容将根据markdown文件中的标题自动生成。

自定义边栏还可以通过设置一个`subMaxLevel`compare [subMaxLevel配置](https://docsify.js.org/#/configuration?id=submaxlevel)来自动生成目录。

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true,
    subMaxLevel: 2
  }
</script>
<script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
```

**git 相关配置**(已在GitHub中配置完成)

**git add .**

**git commit -m'update'**

**git push**



