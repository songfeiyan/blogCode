---
title: 单个gitHub账号添加多个gitHub pages
---
## 问题描述
之前自己写了一个vue项目放在gitHub.io项目下，所以可以通过目录链接访问自己的项目。但是最近基于hexo搭建了自己的博客，也是需要放到gitHub.io项目中的。但是每次通过hexo部署到gitHub之后，都会覆盖整个项目文件的。所以就造成了原来项目丢失，不能访问的问题。 
## 解决方案
gitHub虽然不支持创建多个个人主页，但是支持多个项目主页
个人主页：必须要和用户的gitHub账号同名，所以每个用户有且只能有一个项目主页{% link （userName.gitHub.io）%}
项目主页：命名没有限制{% link （userName.gitHub.io/projectName）%}
## 配置项目主页
（1）新建一个项目，项目名称随意
（2）进入项目，选择settings项，往下拉找到GitHub Pages选择master branch(use the master branch for GitHub pages)
![](/images/page2.png)
## 实例
博客链接： https://songfeiyan.gitHub.io  
项目链接： https://songfeiyan.gitHub.io/vuepro/sfy/dist/index.html
