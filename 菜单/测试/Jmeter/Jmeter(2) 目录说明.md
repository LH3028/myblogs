## Jmeter安装目录说明



<img src="https://gitee.com/myHduwork/myblogimg/raw/master/img/1896874-20200422224200758-446810268.png">



| 文件夹         | 作用                                                        |
| -------------- | ----------------------------------------------------------- |
| bin            | 包含启动、配置等相关命令自己写的脚本默认另存为该目录下      |
| docs           | 官方接口文档，二次开发需要了解的一些接口                    |
| extras         | 辅助库，持续集成会用到（后面讲）                            |
| lib            | 存放各种 Jmeter 核心库的源码 jar 包存放自己二次开发的 jar包 |
| lib\ext        | 官方提供的第三方插件                                        |
| license        | 包含 non-ASF 软件的许可证                                   |
| printable_docs | 离线的帮助文档，可以查看函数等内容                          |
| LICENSE        | JMeter 许可说明                                             |
| NOTICE         | JMeter 简单信息说明                                         |
| README.md      | JMeter 官方基本介绍                                         |



| 文件              | 作用                                                         |
| ----------------- | ------------------------------------------------------------ |
| jmeter.properties | JMeter 核心配置文件，各种配置基本在这完成                    |
| log4j.conf        | JMeter 日志配置管理                                          |
| jmeter.log        | JMeter 运行日志记录，什么输出信息、警告、报错都在这里进行了记录 |
| jmeter.bat        | windows 下 jmeter 的**启动**文件，**带**cmd窗口              |
| jmeterw.cmd       | windows 下 jmeter 的**启动**文件，**不带**cmd窗口            |
| shutdown.cmd      | windows 下 jmeter 的**关闭**文件                             |
| stoptest.cmd      | windows 下 jmeter 停止测试的文件                             |
| jmeter-server.bat | windows 下 jmeter 服务器模式的启动文件                       |
| jmeter-server     | mac 或者 Liunx 分布式压测使用的启动文件                      |