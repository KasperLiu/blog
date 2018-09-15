---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
lastmod: {{ .Date }}
description: ""
tags: []
categories: []

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: false
postMetaInFooter: true
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
# 即可進行inline latex渲染
mathjaxEnableSingleDollar: false
# 公式自动编号
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

# 流程图 
flowchartDiagrams:
  enable: false
  options: ""

# 序列图 see: https://blog.olowolo.com/example-site/post/js-sequence-diagrams/
sequenceDiagrams: 
  enable: false
  options: ""
---

