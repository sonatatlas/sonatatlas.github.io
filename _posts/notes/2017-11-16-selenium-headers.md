---
layout: post
title: 'selenium headers setting'
categories: Spider selenium
---

selenium作为自动化调试工具, 设置headers还是有一些繁琐， 不同的浏览器还需要使用不同的方法, 尝试了chrome和phantomjs设置headers访问数据


##chrome

chrome的稍微简单些

```python
options = webdriver.ChromeOptions()
options.add_argument('user-agent="content of user-agent"')
chrome = webdriver.Chrome(chrome_options=options)
```


phantomjs方法

```python
capability_key= 'phantomjs.page.customHeaders.{}'.format('user-agent')
#字符串还有属性???....这语法搞不懂
webdriver.DesiredCapabilities.PHANTOMJS[capability_key] = 'content of user-agent'
pj = webdriver.PhantomJS()

```