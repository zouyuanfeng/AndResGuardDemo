### 微信资源压缩打包

本工程为新建工程，未修改java代码和资源文件，直接打包后进行微信资源压缩的

介绍可参考之前写的一个[博客](http://blog.csdn.net/u014300915/article/details/50601940)

#### 安装7z
Ubuntu：
```
	$sudo apt-get install p7zip-full
```
windows：
下载地址：[http://www.7-zip.org/](http://www.7-zip.org/)

在win下7Z的安装后如果没有7za.exe的话，可以把7z.exe复制一份改成7za.exe，并配置环境变量 
![图](http://img.blog.csdn.net/20160128171057035)

#### 修改local.properties文件
增加一行：out.apk=/home/zou/app
指定最后apk输出的目录
可不写，主要用于在copyApk方法中


#### 修改settings.gradle
```
def initGradleEnvironment() {
    Properties properties=new Properties();
    File file=new File(rootDir.getAbsolutePath()+"/local.properties")
    properties.load(file.newDataInputStream())
    gradle.ext.sdkDir=properties.getProperty("sdk.dir")
    gradle.ext.outApk=properties.getProperty("out.apk")
}
initGradleEnvironment()
```
读取local.properties文件，并把路径加入到gradle属性中，便于在build.gradle中调用

#### build.gradle文件
编写一个用于压缩的task，通过gradlew  compressApp调用，Linux中./gradlew  compressApp调用，注意，zipalign工具，在build-tools目录下，可根据自己拥有的版本进行修改

#### 调用压缩任务
![log](http://itzyf.qiniudn.com/log.png)
