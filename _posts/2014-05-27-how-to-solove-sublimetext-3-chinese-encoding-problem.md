title: "解决Sublime Text 3中文乱码问题"
date: 2014-05-27 09:13:46
tags: 
- sublime text

---


1.	打开Sublime Text 3，按`Ctrl+～`打开控制行，复制粘贴以下python代码，然后回车运行

``` python
import urllib.request,os,hashlib; h = '7183a2d3e96f11eeadd761d777e62404e330c659d4bb41d3bdf022e94cab3cd0'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

```
2.	重启Sublime Text 3

3.	按`Ctrl+Shift+P`打开命令行，输入`Install Package`，回车，然后继续输入`ConvertToUTF8`，回车
