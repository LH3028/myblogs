### Unittest单元测试



#### 一、什么是unittest

 

unittest 是Python单元测试框架，类似于JUnit框架

unittest中有四个重要的概念：test fixture, test case, test suite , test runner



```
TestCase:
	一个Testcase是的实例就是一个测试用例。什么是测试用例呢？就是一个完整的测试流程，包括测试前准备环境的搭建(setUp)，执行测试代码 (run)，以及测试后环境的还原(tearDown)。元测试(unit test)的本质也就在这里，一个测试用例是一个完整的测试单元，通过运行这个测试单元，可以对某一个问题进行验证

Test suite:
	多个测试用例集合在一起，就是TetsSuite,而且TestSuite也可以嵌套TestSuite.

Test runner:
	是用来执行测试用例的，其中的run(test)会执行TestSuit/TetsCase中的run(result)方法。

TestLoader:
	是用来加载TetsCase到TetsSuite中的，其中有几个loadTestFrom_()方法，就是从各个地方寻找TestCase,创建他们的实例，然后add到TestSuite中，再返回一个TestSuite实例。

Text fixture:
	对一个测试用例环境的搭建和销毁，是一个fixture，通过覆盖 TestCase的setUp()和tearDown()方法来实现。这个有什么用呢？比如说在这个测试用例中需要访问数据库，那么可以在setUp() 中建立数据库连接以及进行一些初始化，在tearDown()中清除在数据库中产生的数据，然后关闭连接。注意tearDown的过程很重要，要为以后的 TestCase留下一个干净的环境。关于fixture，还有一个专门的库函数叫做fixtures，功能更加强大。
```



使用unittets编写Python的单元测试代码，包括如下几个步骤：

1、编写一个Python类，继承unittets模块中的TestCasse类，这就是一个测试类

2、在上面编写的测试类中定义测试方法（这个就是指的测试用例），每个方法的方法名要求以 test 打头，没有额外的参数。 在该测试方法中 调用被测试代码，校验测试结果，TestCase类中提供了很多标准的校验方法，如 最常见的assertEqual。

3、执行 unittest.main() ，该函数会负责运行测试，它会实例化所有TestCase的子类，并运行其中所有以test打头的方法。



#### 二、简单用法

unittest是python自带的一个单元测试框架，类似于java的junit，基本结构是类似的。基本用法如下：

1.用import unittest导入unittest模块

2.定义一个继承自unittest.TestCase的测试用例类，如class xxx(unittest.TestCase):

3.定义setUp和tearDown，这两个方法与junit相同，即如果定义了则会在每个测试case执行前先执行setUp方法，执行完毕后执行tearDown方法。

4.定义测试用例，名字以test开头，unittest会自动将test开头的方法放入测试用例集中。

5.一个测试用例应该只测试一个方面，测试目的和测试内容应很明确。主要是调用assertEqual、assertRaises等断言方法判断程序执行结果和预期值是否相符。

6.调用unittest.main()启动测试

7.如果测试未通过，则会显示e，并给出具体的错误（此处为程序问题导致）。如果测试失败则显示为f，测试通过为.，如有多个testcase，则结果依次显示。



#### 三、unittest模块的常用方法

```python
assertEqual(a, b)   a == b
assertNotEqual(a, b)   a != b
assertTrue(x)   bool(x) is True
assertFalse(x)   bool(x) is False
assertIs(a, b)   a is b
assertIsNot(a, b)   a is not b
assertIsNone(x)   x is None
assertIsNotNone(x)   x is not None
assertIn(a, b)   a in b
assertNotIn(a, b)   a not in b
assertIsInstance(a, b)   isinstance(a, b)
assertNotIsInstance(a, b)   not isinstance(a, b)
```



官网案例：



![img](https://i.loli.net/2020/11/17/U3MJpKSHLsji2xF.png)



#### 五、unittest网易邮箱登录案例



1.打开网易邮箱，写一个简单的登录；

2.判断title完全等于期望结果；

```python
import time
import unittest 
from selenium import webdriver 
from selenium.webdriver.support import expected_conditions as EC 
class mailLogin(unittest.TestCase):
    def setUp(self):
        url = 'https://mail.yeah.net/'
        self.browser = webdriver.Firefox()
        self.browser.get(url)
        time.sleep(5)    def test_login_01(self):
        '''
        用户名、密码为空
        '''
        self.browser.switch_to.frame("x-URS-iframe")
        self.browser.find_element_by_name('email').send_keys('')
        self.browser.find_element_by_name('password').send_keys('')
        self.browser.find_element_by_id('dologin').click()
        self.browser.switch_to.default_content()
        time.sleep(3)
        name = self.browser.find_element_by_id('spnUid')        
        if name == 'sanzang520@yeah.net':
            print('登录成功')        
         else:
            print('登陆失败')    
     def test_login_02(self):
        '''
        用户名正确、密码为错误
        '''
        self.browser.switch_to.frame("x-URS-iframe")
        self.browser.find_element_by_name('email').send_keys('sanzang520')
        self.browser.find_element_by_name('password').send_keys('xxx')
        self.browser.find_element_by_id('dologin').click()
        self.browser.switch_to.default_content()
        time.sleep(3)
        name = self.browser.find_element_by_id('spnUid')       
        if name == 'sanzang520@yeah.net':
            print('登录成功')        
         else:
            print('登陆失败')    
     def test_login_03(self):
        '''
        用户名、密码正确
        '''
        self.browser.switch_to.frame("x-URS-iframe")
        self.browser.find_element_by_name('email').send_keys('sanzang520')
        self.browser.find_element_by_name('password').send_keys('xxx')
        self.browser.find_element_by_id('dologin').click()
        self.browser.switch_to.default_content()
        time.sleep(3)
        name = self.browser.find_element_by_id('spnUid')        
        if name == 'sanzang520@yeah.net':
            print('登录成功')        
        else:
            print('登陆失败')    
     def tearDown(self):
        self.browser.quit()
if __name__ == "__main__":
    unittest.main()


```











