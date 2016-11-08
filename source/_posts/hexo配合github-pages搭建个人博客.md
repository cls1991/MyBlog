title: hexo配合github pages搭建个人博客
date: 2015-11-28 15:53:50
tags:
- hexo
- github pages
- blog
---

1.安装hexo

	npm install hexo-cli -g
	npm install hexo --save

<!-- more -->
2.hexo初始化配置
新建hexo目录, 执行：

	hexo init

新建完成后, 文件目录如下:

	.
	├── _config.yml
	├── package.json
	├── scaffolds
	├── scripts
	├── source
	|      ├── _drafts
	|      └── _posts
	└── themes

3.安装hexo插件

	npm install hexo-generator-index --save
	npm install hexo-generator-archive --save
	npm install hexo-generator-category --save
	npm install hexo-generator-tag --save
	npm install hexo-server --save
	npm install hexo-deployer-git --save
	npm install hexo-deployer-heroku --save
	npm install hexo-deployer-rsync --save
	npm install hexo-deployer-openshift --save
	npm install hexo-renderer-marked@0.2 --save
	npm install hexo-renderer-stylus@0.2 --save
	npm install hexo-generator-feed@1 --save
	npm install hexo-generator-sitemap@1 --save

运行hexo服务

    hexo server            // 或者hexo s

出现下列异常:

    <%- partial('_partial/head') %>
    <%- partial('_partial/header', null, {cache: !config.relative_link}) %>
    <%- body %>
    <% if (theme.sidebar && theme.sidebar !== 'bottom'){ %> <%-     partial('_partial/sidebar', null, {cache: !config.relative_link}) %> <% } %>
    <%- partial('_partial/footer', null, {cache: !config.relative_link}) %>
    <%- partial('_partial/mobile-nav', null, {cache: !config.relative_link}) %> <%-     partial('_partial/after-footer') %>

主要原因是: EJS, Stylus, Marked 组件均被移除, 重新安装以下即可.

解决方案如下:

    npm install hexo-renderer-ejs --save
    npm install hexo-renderer-stylus --save
    npm install hexo-renderer-marked --save

可能会出现以下错误(补充: 2016-11-08 15:35:19):

	Waiting...Fatal error: watch ENOSPC

更新一下组件即可.

	npm dedupe

再运行hexo服务,

    hexo s

默认监听端口为4000, 打开浏览器(http://0.0.0.0:4000), 查看效果.

![hexo_blog.png](https://github.com/cls1991/MyBlog/raw/master/img/hexo_blog.png)

4.hexo简写命令

	hexo n  	# hexo new: 生成文章
	hexo s 	# hexo server: 本地发布预览效果
	hexo g 	# hexo generate: 生成public静态文件
	hexo d    # hexo deploy: 部署到github
