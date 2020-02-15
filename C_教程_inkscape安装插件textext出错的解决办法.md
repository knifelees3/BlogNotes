# inkscape安装插件textext出错的解决办法



## 问题解决:



是因为自己的插件版本于inkscape版本不一致造成的。



## 具体过程



近几日要画一些带公式的矢量图，发现inkscape非常好用，尝试安装插件[textext](https://github.com/textext/textext)时，却出了问题，我直接在该网站下载了最新版，根据[官方教程](https://textext.github.io/textext/#installation-toc)安装了[inkscape0.92.4](https://inkscape.org/release/)以及推荐的[pdf2svg]( https://github.com/textext/pdf2svg/releases (32-bit, 64-bit))



安装好后，开始运行该软件的依赖测试文件 ，接下来就是一连串错误。



**No module named elements or inkex.elements**



当我运行 "setup_win.bat"时，出现以下信息



```bash

Trying to find Inkscape...

Trying registry root HKLM...

Trying registry root HKCU...

Inkscape found as C:\Program Files\Inkscape\inkscape.exe



Trying to detect Python interpreter in Inkscape installation directory...

Success



Trying to run "C:\Program Files\Inkscape\\python.exe" setup.py --inkscape-executable="C:\Program Files\Inkscape\\inkscape.exe" ...



Traceback (most recent call last):

  File "setup.py", line 19, in <module>

    from requirements_check import \

  File "extension\textext/requirements_check.py", line 689, in <module>

    defaults = WindowsDefaults()

  File "extension\textext/requirements_check.py", line 83, in __init__

    import win_app_paths as wap

  File "extension\textext/win_app_paths.py", line 10, in <module>

    import winreg as _wr

ImportError: No module named winreg

```



在网络上找了一遍解决办法之后，我把"win_app_paths.py"文件里面的语句



```bash

import winreg

```

改为了



```bash

import _winreg

```

然后重新开始运行"setup_win.bat"文件，得到如下错误



**[Fail] GTK3 is not found**



```bash

Trying to find Inkscape...

Trying registry root HKLM...

Trying registry root HKCU...

Inkscape found as C:\Program Files\Inkscape\inkscape.exe



Trying to detect Python interpreter in Inkscape installation directory...

Success



Trying to run "C:\Program Files\Inkscape\\python.exe" setup.py --inkscape-executable="C:\Program Files\Inkscape\\inkscape.exe" ...



[TexText][INFO    ]: Using `inkscape-executable` = `C:\Program Files\Inkscape\\inkscape.exe`

[TexText][CRITICAL]: + [Fail] TexText requirements

[TexText][CRITICAL]: /-and-* [Fail] Detect inkscape>=1.0

[TexText][CRITICAL]: |      inkscape>=1.0 is not found (but inkscape=0.92 is found)

[TexText][CRITICAL]: |      Please follow installation instructions at

[TexText][CRITICAL]: |             https://textext.github.io/textext/install/windows.html#windows-install-inkscape

[TexText][CRITICAL]: |      If inkscape is installed in custom location, specify it via

[TexText][CRITICAL]: |             --inkscape-executable=<path-to-inkscape>

[TexText][CRITICAL]: |      and run setup.py again

[TexText][SUCCESS ]: /-and-+ [Succ] Detect *latex

[TexText][SUCCESS ]: |     /--or-* [Succ] `pdflatex.exe` is found at `C:\texlive\2019\bin\win32`

[TexText][SUCCESS ]: |     |      `pdflatex.exe` is found at `C:\texlive\2019\bin\win32`

[TexText][SUCCESS ]: |     /--or-* [Succ] `lualatex.exe` is found at `C:\texlive\2019\bin\win32`

[TexText][SUCCESS ]: |     |      `lualatex.exe` is found at `C:\texlive\2019\bin\win32`

[TexText][SUCCESS ]: |     /--or-* [Succ] `xelatex.exe` is found at `C:\texlive\2019\bin\win32`

[TexText][SUCCESS ]: |            `xelatex.exe` is found at `C:\texlive\2019\bin\win32`

[TexText][SUCCESS ]: /-and-+ [Succ] Detect GUI library

[TexText][INFO    ]:       /--or-* [Fail] GTK3 is not found

[TexText][INFO    ]:       |      Please follow installation instructions at

[TexText][INFO    ]:       |             https://textext.github.io/textext/install/windows.html#windows-install-pygtk2

[TexText][SUCCESS ]:       /--or-* [Succ] TkInter is found

[TexText][ERROR   ]: Automatic requirements check found issue

[TexText][ERROR   ]: Follow instruction above and run install script again

[TexText][ERROR   ]: To bypass requirement check pass `--skip-requirements-check` to setup.py

```



也不清楚问题是否解决，我直接将插件的文件夹“extension”手动复制安装到对应目录"C:\Program Files\Inkscape\share\extensions"，尝试在inkscape运行textext,发现如下错误



**No module named elements **



```bash

[TexText][ERROR   ]: No module named elements

[TexText][ERROR   ]: Traceback (most recent call last):

  File "__init__.py", line 110, in <module>

    import inkex.elements

ImportError: No module named elements



[TexText][INFO    ]: TexText finished with error, please run extension again

[TexText][INFO    ]: If problem persists, please file a bug https://github.com/textext/textext/issues/new



```

我打算向github的作者求助了就在我码完上面的问题描述之后，还有一个选项时要确定各种版本，如下



**System information**



```bash

- TexText version: 

- Inkscape version:

- Operating system: [e.g. Windows 10, 1803, 32-bit]

- SVG-converter installed (pstoedit+ghostscript or pdf2svg):

- GUI framework installed (PyGTK, PyGTK+PyGTK-Sourceview, TkInter):

- Windows only: LaTeX-distribution (MiKTeX, TeX-Live):

- Windows only: TexText installed via batch script or installer file:

```

我才发现我安装的版本时最新的inkscape>1的，我需要安装的textext版本为[0.11.0](https://github.com/textext/textext/releases/tag/0.11.0).



问题终于解决了，希望以后仔细阅读说明。。。。

