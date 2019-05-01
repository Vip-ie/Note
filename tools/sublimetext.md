# Sublime Text3

[官方下载](http://www.sublimetext.com/3)

```
http://www.sublimetext.com/3
```

## [Sublime Text3的插件管理Package Control安装](https://packagecontrol.io)

Sublime Text 3安装Package Control命令

使用Ctrl+\`快捷键或者通过View-&gt;Show Console菜单打开命令行，粘贴如下代码\(注意下面代码为一行\)：

```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

按下enter键,稍等即可,

安装完毕后,重启sublime，此时就可以在Preferences菜单下看到Package Settings和Package Control两个菜单了。

#### Package Control 安装成功的验证

按住Ctrl + shift + p，输入pci你能看到如下界面，就说明你Package Control 安装成功了！



