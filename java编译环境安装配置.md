## 安装JDK

1. 下载安装JDK
2. 配置环境变量：JAVA_HOME，并添加%JAVA_HOME%\bin到PATH
3. 导入证书
   ```
   cd %JAVA_HOME%\bin
   keytool -import -alias mycert -file C:\\path\\to\\mycertificate.cer -keystore "%JAVA\_HOME%\\jre\\lib\\security\\cacerts" -storepass changeit
   ```

## 安装构建工具

1. 下载安装maven
2. 配置环境变量：MAVEN_HOME，并添加%MAVEN_HOME%\bin到PATH
3. 配置镜像
   - 打开`%MAVEN_HOME%\conf\settings.xml`
   - 添加镜像仓库地址

## 安装IDE

1. 下载安装IntelliJ IDEA
2. 导入配置或修改配置
   - 调整 IDE 内存设置：`Help` -> `Change Memory Settings`
   - 配置maven构建：`File` -> `Settings`，`Build, Execution, Deployment` -> `Build Tools` -> `Maven`

## 导入运行项目

1. 打开项目工程
2. 配置SDK：`File` -> `Project Structure`
3. 运行项目
