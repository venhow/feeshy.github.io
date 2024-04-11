---
layout: post
title: 折腾记录：Github Pages页面重定向的实现
date: 2020-10-23
last_modified_at: 2024-04-02
tags:
  - github-pages
  - 重定向
  - 折腾记录
---

## 问题的提出

原名是aaa的页面改成了bbb，`example.github.io/aaaa/aaa.html` 会变成 `example.github.io/aaaa/aaa.html`


由于GH没有开放可配置的标准301重定向，所以只能另寻他法了。



## Jekyll模板跳转




Jekyll官方有一款利用HTTP-REFRESH meta标签跳转的插件[Jekyll Redirect From](https://github.com/jekyll/jekyll-redirect-from)，但不知是有bug，还是GitHub Pages权限问题，从Github Workflow自动编译得到的html文件中并没有出现原本应该自动生成的标签。

可以通过修改页面模板手动实现重定向

Jekyll的 '/_includes' 目录内会有 ，liquid表达式，当front matter

```
{%- if page.redirect.to -%}
<meta http-equiv="refresh" content="1; url={{ page.redirect.to }}">
{%- endif -%}
```

我在模板直接内置了用于跳转的meta标签。在文章的front matter中声明目标网址即可调用：

```
---
redirect_to: www.example.com/new
---
```

这个语法不止适用于站内文章的跳转，也可以跳转到站外的文章，让站外文章享受到与站内文章相同的元数据索引、显示在同一个文章列表。

此外，如果安装了[Jekyll Redirect From](https://github.com/jekyll/jekyll-redirect-from)插件（默认没装），还可以使用插件的语法，在目标文章的front matter声明多个旧地址。插件会自动在列出的旧位置生成front matter含有`redirect_to:`的旧文章

```
---
redirect_from:
  - www.example.com/aaa/old1
  - www.example.com/bbb/old2
---
```

### 跳转页布局

另外，还可以用这个布局创建文章

```
---
layout: redirect
---
```

会进一步增加JavaScript跳转的方法，并在网页附上一个“点击跳转”的链接，再加两重保险。



## 方法二：利用404页面js跳转

把Github Pages的某个原名是aaaa的目录修改成了bbbb，相当于原来的 `example.github.io/aaaa/example.html` 都要变成 `example.github.io/bbbb/example.html` 了。然而一个目录下那么多的文件，总不能一个一个手工设置吧

404 js跳转通用的方法，部署Jekyll编译的静态内容还是直接部署静态内容

缺点，对SEO来说[效果可能不是那么稳定](https://maxket.com/technical-seo-js-redirect/)

在repo的根目录建立一个404.html，用js跳转来曲线救火：

```
window.onload=function() {
    var url = window.location.href
    switch (true) {
        case url.includes('/aaaa'):
            document.location = url.replace('/aaaa', '/bbbb')
            break
}
```

以后每次改目录名就在下面新添一个case就好了

爬虫