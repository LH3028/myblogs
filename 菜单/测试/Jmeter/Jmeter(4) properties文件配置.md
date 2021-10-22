## jmeter.properties

所在目录： E:\apache-jmeter-5.2.1\bin ，jmeter安装目录下的bin目录

**是Jmeter核心配置项文件**

 

### **官方建议**

将需要修改的属性值，复制粘贴到同目录下的 user.properties 

**好处：**当Jmeter升级时，可以避免修改项需要重新应用

 

## 常用的配置

**官方文档：**https://jmeter.apache.org/usermanual/properties_reference.html

### 默认语言设置

- language=en：默认英文
- language=zh_CN：默认中文

**注意：**这个只有在 jmeter.properties 文件中声明才会生效，官方也提醒了

 [![img](https://gitee.com/myHduwork/myblogimg/raw/master/img/1896874-20210521100034954-1463992528.png)](https://img2020.cnblogs.com/blog/1896874/202105/1896874-20210521100034954-1463992528.png)

 

### 配置默认编码格式

- sampleresult.default.encoding=ISO-8859-1：默认ISO-8859-1
- sampleresult.default.encoding=UTF-8：可以改成常用的UTF-8

 

### 输出测试报告模板格式 

jmeter.save.saveservice.output_format=csv

 

### 捕捉cookie

Cookies应该存储为变量

CookieManager.save.cookies=false：默认

CookieManager.save.cookies=true：将cookie存储为变量

 

### 快捷方式（ctrl+数字0-9）

- gui.quick_0=ThreadGroupGui
- gui.quick_1=HttpTestSampleGui
- gui.quick_2=RegexExtractorGui
- gui.quick_3=AssertionGui
- gui.quick_4=ConstantTimerGui
- gui.quick_5=TestActionGui
- gui.quick_6=JSR223PostProcessor
- gui.quick_7=JSR223PreProcessor
- gui.quick_8=DebugSampler
- gui.quick_9=ViewResultsFullVisualizer

 

### post请求，若不添加Content-Type，则不会默认添加Content-type

在5.0版本之前默认是true

post_add_content_type_if_missing=false：默认

post_add_content_type_if_missing=true：添加Content-Type: application/x-www-form-urlencoded

 

### 配置远程主机 host 

remote_hosts=127.0.0.1