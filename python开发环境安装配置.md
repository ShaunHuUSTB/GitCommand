## 安装Python解释器

1. 下载Python安装包并安装
2. 勾选底部的“Add python.exe to PATH”选项

## 配置环境变量和镜像源

1. 安装时若未添加PAH，手动添加Python主目录和Scripts目录到PATH
2. 全局配置pip（推荐，对所有Python项目生效）
   ```
   pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/ 
   pip config set global.trusted-host pypi.tuna.tsinghua.edu.cn
   ```

## 安装配置PyCharm IDE

1. 下载PyCharm并安装
2. Settings -> Project -> Python Interpreter， Add Interpreter添加python解释器
