# python-AI-17-
python+AI笔记(17)
# 一阶-九章-了解异常

# 一阶-九章-异常捕获的方法
#基本捕获语法
try:
    f=open("D:/abc.txt","r",encoding="UTF-8")
except:
    print("出现异常了，文件不存在")
    f=open("D:/abc.txt","w",encoding="UTF-8")

#捕获指定的异常
try:
    print(name)
except NameError as e:  #这里只对name error异常进行捕获，对其他错误类型是不会爆警告的
    print("出现了变量未定义的异常)
    print(e)
    
#捕获多个异常
try:
    1/0
except(NameError,ZeroDivisionError) as e:
    print("出现了变量未定义，=或者除以0异常错误")

#捕获所有异常(第一种基本捕获类型也可以捕获所有错误类型)
try:
    1/0
except Exception as e:
    print("出现异常了")
else:
    print("好高兴，没有异常")
finally:  #finally是无论如何都要执行的代码
    f.close()

# 一阶-九章-异常的传递性
def func1():
    print("func1开始执行")
    num=1/0  #肯定有异常
    print("func1结束执行")

def func2():
    print("func2开始执行")
    func1()
    print("func2结束执行")

def main():
    try:
        func2()
    except Exception as e:
        print(f"出现异常了，异常的信息是{e}")

main()

# 一阶-九章-模块的概念和导入(模块的导入)
#在python中模块就是一个py文件，里面有类、函数、变量等，我们可以导入模块去使用

#使用import导入模块
import time
print("bala")
time.sleep(5)  #睡眠5秒
print("bala")

#通过from 模块名 import 功能名
#通过这种模式就只能使用特定的功能名
from time import sleep
print("bala")
sleep(5)
print("cala)

#使用*导入time模块的所有功能
from time import *  # *也表示所有功能，与第一种的区别是格式
sleep(5)

#使用as给特定功能设置别名
import time as t  #有些模块名字太长给他加别名
print("bala")
t.sleep(5)
print("cala")

#from格式
from time as sl
print("bala")
sl(5)
print("cala")

# 一阶-九章-模块的概念并导入(自定义模块)
#新建一个文件，这个文件就是一个模块，我们可以在这个模块中写入类，函数，变量以便于在其他py文件中进行导入
#如果调用一个同名但是功能不同的函数，则后面的导入会将前面的结果覆盖掉

#__main__变量
#__main__变量在python中就是一个内置变量
def test(a,b):
    print(a+b)
if __name__=='__main__'  #当程序执行到这一步的时候，__name__就会自动转化为'__main__'
    test(1,2)
#这个可以用在在一个模块中运行测试这个函数的功能在主py文件中也不会去执行导入模块的功能

#__all__变量
__all__=['test1']
def test1(a,b):
    print(a+b)

def test2(a,b):
    print(a-b)
#__all__变量的功能就是只在模块中执行test1函数
#__all__变量只在主py文件中用from 模块名 import *中有用
