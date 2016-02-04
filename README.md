### 微信资源压缩打包

本工程为新建工程，未修改java代码和资源文件，直接打包后进行微信资源压缩的

#### 安装7z
```
	$sudo apt-get install p7zip-full
```

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

最后附上之前写的[博客](http://blog.csdn.net/u014300915/article/details/50601940)
