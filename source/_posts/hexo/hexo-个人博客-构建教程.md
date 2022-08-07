---
title: hexo-个人博客 构建教程
date: 2022-08-07 15:44
top: false
cover: true
img: /Assets/Image/hexo.jpg
password:
toc: true
mathjax: true
summary: hexo的个人博客搭建教程 - 包括基础的配置，bug的修复，与github的连接以及 matery主题的简记
tags:
  - hexo
  - gitlab
  - Blog
categories:
  - hexo
---

# hexo-个人博客 构建教程

## Metadata

```yml
- title: hexo-个人博客 构建教程
- date: 2022-08-07 15:44
- version: Version 1
- updateTime: 2022-08-07 17:40
- summary: hexo的个人博客搭建教程 - 包括基础的配置，bug的修复，与github的连接以及 matery主题的简记
- tags:
  - hexo
  - gitlab
  - Blog
- categories:
  - hexo
```

## 前置操作

### 安装 Node.js

1. 下载Node.js。
2. 安装选项全部默认，一路点击Next。
3. 输入node -v和npm -v，如果出现版本号，那么就安装成功了。

### 安装 git

安装选项还是全部默认，只不过最后一步添加路径时选择Use Git from the Windows Command Prompt，这样我们就可以直接在命令提示符里打开git了。

安装完成后在命令提示符中输入git --version验证是否安装成功。

### Github 配置

打开https://github.com/，新建一个项目。

然后如下图所示，输入自己的项目名字，后面一定要加.github.io后缀，README初始化也要勾上。名称一定要和你的github名字完全一样，比如你github名字叫abc，那么仓库名字一定要是abc.github.io。

然后项目就建成了，点击Settings，向下拉到最后有个GitHub Pages，点击Choose a theme选择一个主题。然后等一会儿，再回到GitHub Pages。

点击那个链接，就会出现自己的网页。

### 安装 Hexo

在合适的地方新建一个文件夹，用来存放自己的博客文件。

在终端中，定位到该目录下，输入`npm i hexo-cli -g`安装Hexo。会有几个报错，无视它就行。

安装完后输入`hexo -v`验证是否安装成功。

然后就要初始化我们的网站，输入`hexo init`初始化文件夹，接着输入`npm install`安装必备的组件。

这样本地的网站配置也弄好啦，输入`hexo g`生成静态网页，然后输入`hexo s`打开本地服务器，然后浏览器打开`http://localhost:4000/`。

按`ctrl+c`关闭本地服务器。

### 连接 Github 与 本地

#### git SSH 配置

可参考其他教程，暂不赘述。

#### hexo 连接 github

打开博客根目录下的_config.yml文件，这是博客的配置文件，在这里你可以修改与博客相关的各种信息。

修改最后一行的配置：

```yml
deploy:
  type: git
  repository: https://github.com/【username】/【username】.github.io
  branch: master
```

- 【username】:  替换成 github 的 username

## hexo 的 相关命令

### init

```bash
$ hexo init [folder]
```

新建一个网站。如果没有设置 `folder` ，Hexo 默认在目前的文件夹建立网站。

本命令相当于执行了以下几步：

1.  Git clone [hexo-starter](https://github.com/hexojs/hexo-starter) 和 [hexo-theme-landscape](https://github.com/hexojs/hexo-theme-landscape) 主题到当前目录或指定目录。
2.  使用 [Yarn 1](https://classic.yarnpkg.com/lang/en/)、[pnpm](https://pnpm.js.org/) 或 [npm](https://docs.npmjs.com/cli/install) 包管理器下载依赖（如有已安装多个，则列在前面的优先）。npm 默认随 [Node.js](https://hexo.io/docs/#Install-Node-js) 安装。

### new

```bash
$ hexo new [layout] <title>
```

新建一篇文章。如果没有设置 `layout` 的话，默认使用 [\_config.yml](https://hexo.io/zh-cn/docs/configuration) 中的 `default_layout` 参数代替。如果标题包含空格的话，请使用引号括起来。

```bash
$ hexo new "post title with whitespace"
```

| 参数            | 描述                          |
|---------------|-----------------------------|
| -p, --path    | 自定义新文章的路径                   |
| -r, --replace | 如果存在同名文章，将其替换               |
| -s, --slug    | 文章的 Slug，作为新文章的文件名和发布后的 URL |


默认情况下，Hexo 会使用文章的标题来决定文章文件的路径。对于独立页面来说，Hexo 会创建一个以标题为名字的目录，并在目录中放置一个 `index.md` 文件。你可以使用 `--path` 参数来覆盖上述行为、自行决定文件的目录：

```bash
hexo new page --path about/me "About me"
```

以上命令会创建一个 `source/about/me.md` 文件，同时 Front Matter 中的 title 为 `"About me"`

注意！title 是必须指定的！如果你这么做并不能达到你的目的：

```bash
hexo new page --path about/me
```

此时 Hexo 会创建 `source/_posts/about/me.md`，同时 `me.md` 的 Front Matter 中的 title 为 `"page"`。这是因为在上述命令中，hexo-cli 将 `page` 视为指定文章的标题、并采用默认的 `layout`。

### generate

```bash
$ hexo generate
```

生成静态文件。

| 选项                | 描述                                                                                                       |
|-------------------|----------------------------------------------------------------------------------------------------------|
| -d, --deploy      | 文件生成后立即部署网站                                                                                              |
| -w, --watch       | 监视文件变动                                                                                                   |
| -b, --bail        | 生成过程中如果发生任何未处理的异常则抛出异常                                                                                   |
| -f, --force       | 强制重新生成文件Hexo 引入了差分机制，如果 public 目录存在，那么 hexo g 只会重新生成改动的文件。使用该参数的效果接近 hexo clean &amp;&amp; hexo generate |
| -c, --concurrency | 最大同时生成文件的数量，默认无限制                                                                                        |


该命令可以简写为

```bash
$ hexo g
```

### publish

```bash
$ hexo publish [layout] <filename>
```

发表草稿。

### server

```bash
$ hexo server
```

启动服务器。默认情况下，访问网址为： `http://localhost:4000/`。

| 选项           | 描述              |
|--------------|-----------------|
| -p, --port   | 重设端口            |
| -s, --static | 只使用静态文件         |
| -l, --log    | 启动日记记录，使用覆盖记录格式 |


### deploy

```bash
$ hexo deploy
```

部署网站。

| 参数             | 描述           |
|----------------|--------------|
| -g, --generate | 部署之前预先生成静态文件 |


该命令可以简写为：

```bash
$ hexo d
```

### render

```
$ hexo render <file1> [file2] ...
```

渲染文件。

<table><thead><tr><th>参数</th><th>描述</th></tr></thead><tbody><tr><td><code>-o</code>, <code>--output</code></td><td>设置输出路径</td></tr></tbody></table>

### migrate

```bash
$ hexo migrate <type>
```

从其他博客系统 [迁移内容](https://hexo.io/zh-cn/docs/migration)。

### clean

```bash
$ hexo clean
```

清除缓存文件 (`db.json`) 和已生成的静态文件 (`public`)。

在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

### list

```bash
$ hexo list <type>
```

列出网站资料。

### version

```bash
$ hexo version
```

显示 Hexo 版本。

### 选项

#### 安全模式

```bash
$ hexo --safe
```

在安全模式下，不会载入插件和脚本。当您在安装新插件遭遇问题时，可以尝试以安全模式重新执行。

#### 调试模式

```bash
$ hexo --debug
```

在终端中显示调试信息并记录到 `debug.log`。当您碰到问题时，可以尝试用调试模式重新执行一次，并 [提交调试信息到 GitHub](https://github.com/hexojs/hexo/issues/new)。

#### 简洁模式

```bash
$ hexo --silent
```

隐藏终端信息。

#### 自定义配置文件的路径

```bash
$ hexo server --config custom.yml


$ hexo generate --config custom.yml,custom2.json,custom3.yml
```

自定义配置文件的路径，指定这个参数后将不再使用默认的 `_config.yml`。  
你可以使用一个 YAML 或 JSON 文件的路径，也可以使用逗号分隔（无空格）的多个 YAML 或 JSON 文件的路径。例如：

```bash
$ hexo server --config custom.yml


$ hexo generate --config custom.yml,custom2.json,custom3.yml
```

当你指定了多个配置文件以后，Hexo 会按顺序将这部分配置文件合并成一个 `_multiconfig.yml`。如果遇到重复的配置，排在后面的文件的配置会覆盖排在前面的文件的配置。这个原则适用于任意数量、任意深度的 YAML 和 JSON 文件。

#### 显示草稿

```bash
$ hexo --draft
```

显示 `source/_drafts` 文件夹中的草稿文章。

#### 自定义-CWD

```bash
$ hexo --cwd /path/to/cwd
```

自定义当前工作目录（Current working directory）的路径。

## 个性化定义

### hexo-theme-matery 主题

[点我跳转](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md)

## BUG 及 解决

## 更新日志

### Version 1

**Done**

- 创建笔记
- 简单的介绍

**TODO**

- Matery 主题的介绍
- Bug及解决

## 参考文献

- [超详细Hexo+Github博客搭建小白教程](https://godweiyang.com/2018/04/13/hexo-blog/#toc-heading-1)
    - 韦阳的博客
    - 前置条件
- [指令](https://hexo.io/zh-cn/docs/commands)
    - hexo 官网
    - hexo 的指令
- [hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md)
    - matery - github
    - matery 主题
