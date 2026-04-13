# PyInstaller Extractor

> 原项目地址：https://github.com/extremecoders-re/pyinstxtractor  
> 使用 [pyinstxtractorCN.py](pyinstxtractorCN.py) 以中文输出（帮助，提示，报错）


PyInstaller Extractor 是一个 Python 脚本，用于提取由 PyInstaller 生成的可执行文件内容。

脚本会自动修复提取出的 pyc 文件头，以便 Python 字节码反编译器正确识别。脚本可运行在 Python 2.x 和 3.x。PyInstaller 2.0、2.1、3.0、3.1、3.2、3.3、3.4、3.5、3.6、4.0、4.1、4.2、4.3、4.4、4.5、4.5.1、4.6、4.7、4.8、4.9、4.10、5.0、5.0.1、5.1、5.2、5.3、5.4、5.4.1、5.5、5.6、5.6.1、5.6.2、5.7.0、5.8.0、5.9.0、5.10.0、5.10.1、5.11.0、5.12.0、5.13.0、5.13.1、5.13.2、6.0.0、6.1.0、6.2.0、6.3.0、6.4.0、6.5.0、6.6.0、6.7.0、6.8.0、6.9.0、6.10.0、6.11.0、6.11.1、6.12.0、6.13.0、6.14.0、6.14.1、6.14.2、6.15.0、6.16.0、6.17.0、6.18.0、6.19.0 均已[测试](https://github.com/pyinstxtractor/pyinstxtractor-test-binaries)并支持。理论上其他版本也可能可用。

该项目最初托管于 [SourceForge](https://sourceforge.net/projects/pyinstallerextractor/)。

## 用法

传入 exe 文件路径即可运行：

```bash
$ python pyinstxtractor.py <filename>
C:\>python pyinstxtractor.py <filename>
```

建议使用与目标可执行文件打包时相同版本的 Python 来运行脚本，以减少提取 `PYZ` 归档时可能出现的反序列化错误。

## 本 Fork 新增参数

- `-i PATH`, `--interpreter PATH`  
  指定一个 Python 解释器，用于反序列化 `PYZ TOC`。当当前解释器版本与目标包版本不一致时可使用该参数。

- `-f`, `--force`  
  当版本不一致时，强制使用当前解释器尝试反序列化 `PYZ`。

脚本在无参数运行时会打印完整帮助和参数说明。

## 示例

```text
X:\> python pyinstxtractor.py test.exe
[+] Processing dist\test.exe
[+] Pyinstaller version: 2.1+
[+] Python version: 36
[+] Length of package: 5612452 bytes
[+] Found 59 files in CArchive
[+] Beginning extraction...please standby
[+] Possible entry point: pyiboot01_bootstrap.pyc
[+] Possible entry point: test.pyc
[+] Found 133 files in PYZ archive
[+] Successfully extracted pyinstaller archive: dist\test.exe

You can now use a python decompiler on the pyc files within the extracted directory
```

提取 pyc 文件后，可使用 [Uncompyle6](https://github.com/rocky/python-uncompyle6/) 和 [Decompyle++](https://github.com/zrax/pycdc) 等反编译器。

```text
X:\> uncompyle6.exe test.exe_extracted\test.pyc
X:\> uncompyle6.exe test.exe_extracted\PYZ-00.pyz_extracted\__future__.pyc
```

## 提取 Linux ELF 二进制

Pyinstxtractor 可以原生提取 Linux ELF 二进制文件，无需额外工具。

更多信息请查看 [Wiki](https://github.com/extremecoders-re/pyinstxtractor/wiki/Extracting-Linux-ELF-binaries) 和 [FAQ](https://github.com/extremecoders-re/pyinstxtractor/wiki/Frequently-Asked-Questions)。

## 相关项目

- [pyinstxtractor-ng](https://github.com/pyinstxtractor/pyinstxtractor-ng):  
  pyinstxtractor 的独立二进制版本。该工具无需 Python 运行，可提取所有支持版本的 PyInstaller，也支持加密的 pyinstaller 可执行文件。
- [pyinstxtractor-web](https://github.com/pyinstxtractor/pyinstxtractor-go):  
  基于 Go 与 GopherJS 的浏览器版 pyinstxtractor。

## 许可证

GNU General Public License v3.0
