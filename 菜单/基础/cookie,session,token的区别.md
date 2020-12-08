## Cookie ,session,token的区别







Cookie的内容是保存一小段文本信息，这些文本信息组成一份通行证。它是客户端对于无状态协议的一种解决方案。

**Cookie的原理**

（1）客户端第一次请求时，发送数据到服务器。

（2）服务器返回响应信息的同时，还会传回一个cookie（cookie S-001）

（3）客户端接收服务器的响应之后，浏览器会将cookie存放在一个统一的位置。

（4）客户端再次向服务器发送请求的时候，会把Cookie S-001再次发挥服务器。

![img](https://img2018.cnblogs.com/blog/1779991/201908/1779991-20190828115154845-1647356501.png)

**cookie的生命周期**

cookoe的生存时间是整个会话期间：浏览器会将cookie保存在内存中，浏览器关闭时自动删除这个cookie

cookie的生存时间是长久有效的：手动将cookie报存在客户端的硬盘中，浏览器关闭的话，cookie页不会清除；下次在打开浏览器访问对应网站内容，这个cookie就会自动再次发送到服务器。

**session的原理：**

（1）服务器在处理客户端请求过程中会创建session，并且为该session生存唯一的session ID。（这个session ID在随后的请求中会被用来重新获得已经创建的session。在session被创建后，就可以调用session相关的方法向session中新增内容，这些内容只会保存在服务器中） 

（2）服务器将session ID发送到客户端

（3）当客户端再次请求时，就会带上这个session ID

（4）服务器接收到请求之后就会一句Session ID 找到相应的Session ，完成请求

ps：1、虽然session保存在服务器，但它还是需要客户端浏览器的支持，因为session需要使用cookie作为识别标志。服务器会向客户端发送一个名为JSEDDIONID的cookie，它的值为session ID。

​    2、当cookie被禁用时，可以使用url重写的方法：将session写在URL中，服务器在进行解析

![img](https://img2018.cnblogs.com/blog/1779991/201908/1779991-20190828115645126-1101344557.png)

**session的生命周期：**

与cookie一直，服务器也能设置session的生效时间。

**cookie和session的区别**

**1、存储位置不同**：session存储在服务器，cookie存储在客户端

**2、存储容量不同：**单个cookie保存数据小于等于4kb，一个站点最多保存20个cookie；session没有上限，但是由于服务器内存性能考虑，session不要存太多东西，并有删除机制

**3、存取方式不同：**cookie只能保存ASCII字符串；session能存取任何类型的数据

**4、隐私策略不同：**cookie是对客户端是可见的，可以分析存放在本地的cookie并进去cookie欺骗；session存储在服务器上，对于客户端是透明的，不存在敏感信息泄露的风险

**5、服务器压力不同：**session是保存在服务端，每隔用户都会产生一个session。加入并发访问的用户太多，会产生很多的session，对服务器是一个很大的负担，耗费大量内存

​                  cookie保管在客户端，不占用服务器资源。对于并发用户十分多的网站，session是一个很好的选择。

**6、浏览器的支持不同：**session不支持新建窗口，只支持字窗口。而cookie都支持。 

​                   假设浏览器禁用cookie，session可以通过URL重写的方法实现。COOKIE就派不上用场。

**Token的原理：**

（1）客户端第一次请求时，发送用户信息到服务器。服务器对用户信息使用HSA256算法及密钥进行签名，再将这个签名和数据一起作为token返回给客户户端。

（2）服务端不再保存token，客户端保存token。

（3）当客户端再次发送请求时，在请求信息中将token一起发送给服务器。

（4）服务器用同样的HSA256算法和密钥，对数据再计算一次签名，和token的签名做比较

（5）如果相同，服务器就知道客户端登录过，则反之。





