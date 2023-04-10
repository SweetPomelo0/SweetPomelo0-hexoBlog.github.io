---
title: hexo+Github博客教程
date: 2023/4/10
updated: 2023/4/10
tags: 配置
categories: 环境配置
keywords: hexo Github 博客
description: hexo+Github搭建博客教程
comments: false
cover: /img/bg3.png
---



# 1.引言

🔧使用的工具及环境

* hexo + GitHub + beatify 
* 系统: Mac

# 2.hexo博客框架

## 2.1 hexo简介

hexo是基于node.js的静态博客网站生成器，主要有以下优点：

* 支持md语法
* 能够快速生成静态html文件
* 部署容易，接口简单
* 社区主题、插件很多

## 2.2 环境配置

首先需要node.js环境，可以直接从官网下载，网址https://nodejs.org/zh-cn

node -v 能够查到版本信息，就可以了

## 2.3 生成博客

* 安装hexo命令：`npm install hexo-cli -g`,表示全局安装hexo命令行工具

* 新建文件夹，在其目录下初始化：`hexo init xxx`,xxx写你的博客目录名称

  ![image-20230407195404947](https://raw.githubusercontent.com/SweetPomelo0/picGo/main/img/202304071954699.png)

* 进入博客目录：`cd xxx` 

* 安装博客需要的其他支持：`npm install`

* 文件目录如下：

![image-20230407195905451](https://raw.githubusercontent.com/SweetPomelo0/picGo/main/img/202304071959024.png)

* 生成新文章

  ```bash
  hexo new post "test" # 会在 source/_posts/ 目录下生成文件 ‘test.md’，打开编辑
  hexo generate        # 生成静态HTML文件到 /public 文件夹中
  hexo server          # 本地运行server服务预览，打开http://localhost:4000即可预览博客
  ```

* 界面如下，更多主题查看官网https://hexo.io/themes/

  ![image-20230407200202049](https://raw.githubusercontent.com/SweetPomelo0/picGo/main/img/202304072002191.png)

* 为了后续netlify建站方便，在`package.json`中添加一个命令

  ```json
  {
      // ......
      "scripts": {
          "build": "hexo generate",
          "clean": "hexo clean",
          "deploy": "hexo deploy",
          "server": "hexo server",
          "netlify": "npm run clean && npm run build" // 这一行为新加
      },
      // ......
  }
  ```

* `_congif.yaml`的字段含义

  ```yml
  # Site
  title: Hexo  # 网站标题
  subtitle:    # 网站副标题
  description: # 网站描述
  author: John Doe  # 作者
  language:    # 语言
  timezone:    # 网站时区, Hexo默认使用您电脑的时区
  
  # URL
  ## If your site is put in a subdirectory, set url as 'http://yoursite.com/child'
  ## and root as '/child/'
  url: http://yoursite.com   # 你的站点Url
  root: /                    # 站点的根目录
  permalink: :year/:month/:day/:title/   # 文章的 永久链接 格式   
  permalink_defaults:        # 永久链接中各部分的默认值
  
  # Directory   
  source_dir: source     # 资源文件夹，这个文件夹用来存放内容
  public_dir: public     # 公共文件夹，这个文件夹用于存放生成的站点文件。
  tag_dir: tags          # 标签文件夹     
  archive_dir: archives  # 归档文件夹
  category_dir: categories     # 分类文件夹
  code_dir: downloads/code     # Include code 文件夹
  i18n_dir: :lang              # 国际化（i18n）文件夹
  skip_render:                 # 跳过指定文件的渲染，您可使用 glob 表达式来匹配路径。    
  
  # Writing
  new_post_name: :title.md  # 新文章的文件名称
  default_layout: post      # 预设布局
  titlecase: false          # 把标题转换为 title case
  external_link: true       # 在新标签中打开链接
  filename_case: 0          # 把文件名称转换为 (1) 小写或 (2) 大写
  render_drafts: false      # 是否显示草稿
  post_asset_folder: false  # 是否启动 Asset 文件夹
  relative_link: false      # 把链接改为与根目录的相对位址    
  future: true              # 显示未来的文章
  highlight:                # 内容中代码块的设置    
    enable: true            # 开启代码块高亮
    line_number: true       # 显示行数
    auto_detect: false      # 如果未指定语言，则启用自动检测
    tab_replace:            # 用 n 个空格替换 tabs；如果值为空，则不会替换 tabs
  
  # Category & Tag
  default_category: uncategorized
  category_map:       # 分类别名
  tag_map:            # 标签别名
  
  # Date / Time format
  ## Hexo uses Moment.js to parse and display date
  ## You can customize the date format as defined in
  ## http://momentjs.com/docs/#/displaying/format/
  date_format: YYYY-MM-DD     # 日期格式
  time_format: HH:mm:ss       # 时间格式    
  
  # Pagination
  ## Set per_page to 0 to disable pagination
  per_page: 10           # 分页数量
  pagination_dir: page   # 分页目录
  
  # Extensions
  ## Plugins: https://hexo.io/plugins/
  ## Themes: https://hexo.io/themes/
  theme: landscape   # 主题名称
  
  # Deployment
  ## Docs: https://hexo.io/docs/deployment.html
  #  部署部分的设置
  deploy:     
    type: '' # 类型，常用的git 
  ```

# 3.Github项目文件托管

  ```bash
  cd "博客目录"
  git init
  git add .
  git commit -m "my blog first commit"
  git remote add origin "远端github仓库地址"
  git branch -M main
  git push -u origin main
  ```
# 4.Netlify建站



* 首先注册登录，网址https://app.netlify.com/

* 选择sites-import an existion project

  ![image-20230407201907241](https://raw.githubusercontent.com/SweetPomelo0/picGo/main/img/202304072019278.png)

* 选择刚刚上传的博客项目，一切默认，处理构建命令改成`npm run netlify`

  ![image-20230407202819668](https://raw.githubusercontent.com/SweetPomelo0/picGo/main/img/202304072028742.png)

* 构建完成，就可以看到个人博客的URL。如果有域名，可以继续配置域名



  # 5.主题配置

* 我使用的主题是Bufferfly：https://butterfly.js.org/posts/21cfbf15/

  ```bash
  git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
  ```

* 修改`_config.yml`

  ```bash
  theme: butterfly
  ```

* 安装插件

  ```bash
  npm install hexo-renderer-pug hexo-renderer-stylus --save
  ```

* 一些用在md文件的参数

  * Page Front-matter：用于页面配置

    ```bash
    ---
    title: #必需：页面标题
    date: #必需：页面创建日期
    type: #必需：标签、分类和友情链接三个页面需要配置
    updated: #页面更新日期
    description: #页面描述
    keywords: #页面关键字
    comments: #显示页面评论模块
    top_img: #页面顶部图片
    mathjax: #显示mathjax(当设置mathjax的per_page:false时，才需要配置，默认false)
    katex: #显示katex(当设置katex的per_page: false时，才需要配置，默认 false)
    aplayer: #在需要的页面加载aplayer的js和css,请参考文章下面的音乐 配置
    highlight_shrink: #配置代码框是否展开(true/false)(默认为设置中highlight_shrink的配置)
    aside:#显示侧边栏 (默认 true)
    ---
    ```

  * Post Front-matter：用于文章页配置

    ```bash
    ---
    title: #必需：文章标题
    date: #必需：文章创建日期
    updated:#文章更新日期
    tags:#文章标签
    categories:#文章分类
    keywords:#文章关键字
    description:#文章描述
    top_img:#文章顶部图片
    comments:#显示文章评论模块(默认 true)
    cover:#文章缩略图(如果没有设置top_img,文章页顶部将显示缩略图，可设为false/图片地址/留空)
    toc:#显示文章TOC(默认为设置中toc的enable配置)
    toc_number:#显示toc_number(默认为设置中toc的number配置)
    toc_style_simple:#显示 toc 简洁模式
    copyright:#显示文章版权模块(默认为设置中post_copyright的enable配置)
    copyright_author:#文章版权模块的文章作者
    copyright_author_href:#文章版权模块的文章作者链接
    copyright_url:#文章版权模块的文章链接
    copyright_info:#文章版权模块的版权声明文字
    mathjax:#显示mathjax(当设置mathjax的per_page: false时，才需要配置，默认 false)
    katex:#显示katex(当设置katex的per_page: false时，才需要配置，默认 false)
    aplayer:#在需要的页面加载aplayer的js和css,请参考文章下面的音乐 配置
    highlight_shrink:#配置代码框是否展开(true/false)(默认为设置中highlight_shrink的配置)
    aside:#显示侧边栏 (默认 true)
    ---
    ```

* 创建标签页、分类页、友情链接、图库、子页面等见文档

  



















