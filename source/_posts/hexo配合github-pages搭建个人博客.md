title: hexo配合github pages搭建个人博客
date: 2015-11-28 15:53:50
tags:
- hexo
- github pages
- blog
---

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

再运行hexo服务, 

    hexo s

默认监听端口为4000, 打开浏览器(http://0.0.0.0:4000), 查看效果.

![hexo_blog.png](https://github.com/cls1991/MyBlog/raw/master/img/hexo_blog.png)
