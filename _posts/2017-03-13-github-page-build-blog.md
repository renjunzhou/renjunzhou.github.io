---
layout: post
title: Building a BLOG by Github Pages
---
#0. Introducdion
#1. Godaddy 购买域名
Not necessary
#2. 配置Github
##2.1 Create a repository
Head over to GitHub and create a new repository named username.github.io, where username is your username (or organization name) on GitHub.
If the first part of the repository doesn’t exactly match your username, it won’t work, so make sure to get it right.

##2.2 Clone the repository
Click the "Set up in Desktop" button. When the GitHub desktop app opens, save the project.
If the app doesn't open, launch it and clone the repository from the app.

##2.3 Create an index file
Grab your favorite text editor and add an index.html file to your project:

  index.html
  <!DOCTYPE html>
  <html>
  <body>
  <h1>Hello World</h1>
  <p>I'm hosted with GitHub Pages.</p>
  </body>
  </html>

##2.4 Commit & sync
Enter the repository, commit your changes, and press the sync button.

##2.5 …and you're done!
Fire up a browser and go to http://username.github.io.

#3. 绑定域名到GitHub Pages
(绑定到DNSpod会有https警告，可绑定到4提供的服务商)
[GitHub帮助文档](https://help.github.com/articles/quick-start-setting-up-a-custom-domain/)

##3.1
Pick a custom domain and register it with a DNS provider (if you haven't already done so). A DNS provider is a company that allows users to buy and register a unique domain name and connect that name to an [IP (Internet Protocol) address](https://en.wikipedia.org/wiki/IP_address) by pointing your domain name to an IP address or a different domain name. A DNS provider may also be called a domain registrar or DNS host.

##3.2
[Add your custom domain to your GitHub Pages site.](https://help.github.com/articles/adding-or-removing-a-custom-domain-for-your-github-pages-site)

##3.3
Set up your custom domain with your DNS provider. Our guides outline how to set up your pages custom domain with your DNS provider depending on the type of custom domain you have:
[Setting up an apex domain](https://help.github.com/articles/setting-up-an-apex-domain) such as example.com
[Setting up a www subdomain](https://help.github.com/articles/setting-up-a-www-subdomain) such as www.example.com
[Setting up an apex domain and www subdomain](https://help.github.com/articles/setting-up-an-apex-domain-and-www-subdomain) such as example.com and www.example.com
[Setting up a custom subdomain](https://help.github.com/articles/setting-up-a-custom-subdomain) such as blog.example.com

#4. Open https
[Guide](https://zhuanlan.zhihu.com/p/22667528)

#5. Install Jekyll
[Jekyll DOC]https://jekyllrb.com/docs/quickstart/
#5.1 Install Ruby
#5.2 Install Jekyll
  # Install Jekyll and Bundler gems through RubyGems
  ~ $ gem install jekyll bundler
  # Create a new Jekyll site at ./myblog
  ~ $ jekyll new myblog
  # Change into your new directory
  ~ $ cd myblog
  # Build the site on the preview server
  ~/myblog $ bundle exec jekyll serve
  # Now browse to http://localhost:4000
#5.3 Another way 
sudo gem install github-pages，安装 Jekyll
之后你需要在 master 下新建一个 file，命名为 Gemfile，输入

source 'https://rubygems.org'
gem 'github-pages'

运行 terminal，使用命令行移至 repository 根目录下 (也可以直接在 GitHub Desktop 下右键 repository 打开)
之后运行

bundle exec jekyll serve

下面，就可以使用 Jekyll 啦，本地测试在浏览器输入 http://localhost:4000 即可(本地测试结束后 commit to master 提交线上即可)
