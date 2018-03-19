---
title: hexo localhost:4000空白页面
---
## 问题描述
个人的blog源码放在了个人的gitHub上面，当git clone源码，执行hexo server之后，报错No layout: index.html，而且localhost:4000是空白页
## 解决方案
这其实是因为git clone之后，theme文件下的主题文件下载下来，查看项目下面的theme下面的主题文件是空的，所以需要重新git clone对应主题文件
