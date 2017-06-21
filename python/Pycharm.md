## Pycharm 安装autopep8
autopep8为python的一个自动排版工具，具体步骤为：
### 安装autopep8
```
pip install autopep8
```

### 配置参数
#### windows  
打开Pycharm -> File -> settings -> Tools -> Extends Tools -> 添加

* program: autopep8.exe
* parameters: --in-place --aggressive --aggressive $FilePath$
* working dir: 具体的程序所在路径
* Outpu Files：$FILE_PATH$\:$LINE$\:$COLUMN$\:.*

#### mac
打开Pycharm -> preferences - Tools -> Extends Tools -> +

* Name: autopep8
* Program: autopep8
* Parameters: --in-place --aggressive --aggressive $FilePath$
* Working directory: /Library/Frameworks/Python.framework/Versions/3.6/bin/
* Outpu Files: $FILE_PATH$\:$LINE$\:$COLUMN$\:.*

-- autopep8可以通过which命令去获取Program以及Working directory.

#### 以上步骤完成后就可以通过右键找到：External Tools -> Autopep8