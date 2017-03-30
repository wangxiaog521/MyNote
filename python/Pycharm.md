# Pycharm 安装autopep8
autopep8为python的一个自动排版工具，具体步骤为：
## 安装autopep8
```
pip install autopep8
```

## 打开Pycharm -> File -> settings -> Tools→Extends Tools -> 添加
* program: autopep8.exe
* parameters: --in-place --aggressive --aggressive $FilePath$
* working dir: 具体的程序所在路径
* Outpu Files：$FILE_PATH$\:$LINE$\:$COLUMN$\:.*

## 以上步骤完成后就可以通过右键找到：External Tools -> Autopep8