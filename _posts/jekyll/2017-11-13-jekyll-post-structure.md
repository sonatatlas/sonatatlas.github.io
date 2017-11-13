---
layout: post
title: "Jekyll日志结构探索"
date: "2017-11-13"
categories: jekyll useJekyll
---

我正在编辑的是`kramdown`为引擎的`markdown`文件, 上面有一个这样的yaml解析头, 在文本编辑过程中, 我们需要使用[kramdown]语法.


```
---
layout: post
title: "Jekyll日志结构探索"
date: "2017-11-13"
categories: jekyll usejekyll
---
```


### kramdown config
+ layout: post

  [Jekyll Doc]解释道, layout提供了三个内置的选择`pages`, `posts`, `drafts`, 三种不同的markdown渲染模式

+ title: "Jekyll文件结构探索"

  这个表意很清楚, 就是我们正在写的这个MarkDown解析成html后的title

+ date: '2017-11-13'

  日期有一点我不太明白, 我看了`bundle`好的`guid markdown`，他的日期是完整的`utc time`格式, 除去通过输入法输入这样完整的日期, 手动输入是很麻烦的， 不知道是否可以自动生成

+ categories: jekyll jekyll

  这个标注了我们的`MarkDown`储存位置, 我在下面描述一下我的发现,也可以翻一翻官方的解释[Jekyll Post Doc]

### 本篇文章的文件关联

```
.
├── _posts
|    └──jekyll
|	└──2017-11-13-jekyll-post-structure.md
└── _site
    └──jekyll
        └──useJekyll/2017/11/13/jekyll-post-structure.html
```

看了上面的文件结构, 多少会对`Jekyll`的post结构有些了解吧~

正如Jekyll所说的, 不需要数据库， Jekyll非常强大, 动态增删渲染文件! 这完全激起了我对ruby学习的兴趣!


__MarkDown的文件名必须是`2017-11-13-xxx.md`这样的格式, 否则会无法解析出去~__


[kramdown]: https://kramdown.gettalong.org
[Jekyll Doc]: https://jekyllrb.com/docs/configuration/#front-matter-defaults
[Jekyll Post Doc]: https://jekyllrb.com/docs/posts/