title: sublime text软件配置
date: 2015-11-17
tags: 软件配置
---

### sublime Text2/3 软件配置

#### 1.下载安装软件；

#### 2.破解
在help --> enter license 中输入注册码：
>----- BEGIN LICENSE -----
Andrew Weber
Single User License
EA7E-855605
813A03DD 5E4AD9E6 6C0EEB94 BC99798F
942194A6 02396E98 E62C9979 4BB979FE
91424C9D A45400BF F6747D88 2FB88078
90F5CC94 1CDC92DC 8457107A F151657B
1D22E383 A997F016 42397640 33F41CFC
E1D0AE85 A0BBD039 0E9C8D55 E1B89D5D
5CDB7036 E56DE1C0 EFCC0840 650CD3A6
B98FC99C 8FAC73EE D2B95564 DF450523
------ END LICENSE ------

#### 3.安装 package control。
打开控制台（ctrl+ ~），输入安装代码。
*Sublime Text 3:*
``` phython
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

*Sublime Text 2:*
``` phython
import urllib2,os; pf='Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler( ))); open( os.path.join( ipp, pf), 'wb' ).write( urllib2.urlopen( 'http://sublime.wbond.net/' +pf.replace( ' ','%20' )).read()); print( 'Please restart Sublime Text to finish installation')
```

#### 4.安装主题
首先安装在package control中安装theme-brogrammer；然后在preferencs-->Color Scheme中配选择Theme-Brogrammer-->brogrammer；最后在preferences-->Setting-User中加入以下配置：
``` json
{
  "theme": "Brogrammer.sublime-theme",
  "color_scheme": "Packages/Theme - Brogrammer/brogrammer.tmTheme"
}
```

#### 5.安装插件
- `emmet`：代码提示
- `theme-brogrammer`：sublime Text主题[（github地址）](https://github.com/kenwheeler/brogrammer-theme)
- `pretty json`：格式化json数据（热键Ctrl+Alt+j）
- `scss高亮`： [MarioRicalde/SCSS.tmbundle](https://github.com/MarioRicalde/SCSS.tmbundle)


#### 附录
- 在linux下安装sublime Text 3。可以通过PPA方式来在ubuntu系统下安装，安装方法：
>sudo add-apt-repository ppa:webupd8team/sublime-text-3
sudo apt-get update
sudo apt-get install sublime-text-installer