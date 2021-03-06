学习资料库
http://www.xuexi111.com/book/jisuanji/70029.html
#### SICP
https://mitpress.mit.edu/sicp/

https://i2p.kimleo.net/

http://llvm.org/docs/ProgrammersManual.html
http://llvm.org/docs/CodingStandards.html
##### 你读过的最好的 C++ 开源代码是什么？
https://www.zhihu.com/question/21376384
#####　google C++规范
http://google.github.io/styleguide/cppguide.html

http://xuyangkang.github.io/blogs/c_trivia.html

##### 高速上手 C++ 11/14
https://changkun.gitbooks.io/cpp1x-tutorial/content/7-thread.html

##### C++并发编程(中文版) c++11
https://www.gitbook.com/book/chenxiaowei/cpp_concurrency_in_action/details

程序员的自我修养（五）：C++ 多线程编程初步
https://liam0205.me/2017/05/16/first-step-on-multithread-programming-of-cxx/

#####　C++ 11 --17
http://en.cppreference.com/w/cpp/compiler_support

##### 使用 C++11 编写 Linux 多线程程序
https://www.ibm.com/developerworks/cn/linux/1412_zhupx_thread/index.html


##### C++ 11 多线程--线程管理
http://www.cnblogs.com/wangguchangqing/p/6134635.html

##### 漫谈c++11 Thread库之使写多线程程序
http://www.cnblogs.com/ittinybird/p/4820142.html

C++ 并发编程（一）：创建线程
https://segmentfault.com/a/1190000006232497

C++ 线程同步的四种方式
http://blog.jobbole.com/109200/

三种线程池
https://github.com/lizhenghn123/zl_threadpool/tree/master/ThreadPoolCpp11

非常精简的Linux线程池实现（一）——使用互斥锁和条件变量
http://blog.csdn.net/kxcfzyk/article/details/31719687

[C++]C++ 100行实现线程池
http://chestnutheng.cn/2017/04/07/cpp-threadpool/

各种语言性能对比
http://benchmarksgame.alioth.debian.org/

C 程序性能优化技巧
http://xuyangkang.github.io/blogs/c_trivia.html

深入研究 C++中的 STL Deque 容器
http://www.yesky.com/100/1889600.shtml
https://www.zhihu.com/question/26091467

(原创)c++11改进我们的模式之改进观察者模式
https://www.cnblogs.com/qicosmos/p/3145585.html
C++11实现观察者模式
http://blog.csdn.net/xfgryujk/article/details/69485982
设计模式之观察者模式（c++）
http://blog.csdn.net/wuan584974722/article/details/72865925
http://www.169it.com/blog_article/4191897772.html
http://blog.csdn.net/wuzhekai1985/article/details/6674984

http://blog.csdn.net/xiaonaiquan/article/details/78474811
##### libuv C++封装
http://download.csdn.net/download/liuxlyangjl_01/9454331

如何使用C++11实现跨平台的定时器timer？
https://www.zhihu.com/question/38427301
高性能服务器开发之C++定时器
http://www.cnblogs.com/junye/p/5836552.html
https://github.com/pp-qq/timer
https://www.ibm.com/developerworks/cn/linux/l-cn-timers/index.html
##### setitimer()为Linux的API
https://www.cnblogs.com/dandingyy/articles/2653218.html
##### 异步 回调 事件循环

异步，就是一个事情，要分好成好几块，比如分成 A、B、C、D 来并行做，但A做到一半，要等着用到C做完后的结果，再进行下去。这样就是异步完成这个事情。诸如此类。A的结果又要传给B，这样，A在加调C之前，会有一个闭包，把A做到一半的现场环境保存下来，回调C。

####详解回调函数——以JS为例解读异步、回调和EventLoop
http://blog.csdn.net/tywinstark/article/details/48447135

##### C++并发指南系列
http://www.cnblogs.com/haippy/p/3284540.html

https://zh.wikipedia.org/zh-cn/C%2B%2B11
云风的博客
https://blog.codingnow.com/

[转]史上最快消息内核——ZeroMQ
http://itindex.net/detail/4067-%E6%B6%88%E6%81%AF-%E5%86%85%E6%A0%B8-zeromq
那些年我们追过的网络库
https://bbs.avplayer.org/t/topic/654
Muduo 网络编程示例之二：Boost.Asio 的聊天服务器
http://www.cppblog.com/Solstice/archive/2011/02/04/139718.html

http://llvm.org/docs/Coroutines.html

===========================================================

##### 支持nullptr
```
 g++ -std=gnu++0x -o t1  t1.c
```
t1.c
```
#include <iostream>
void foo(char *);
void foo(int);
int main() {

    if(NULL == (void *)0) std::cout << "NULL == 0" << std::endl;
    else std::cout << "NULL != 0" << std::endl;

    foo(0);
    // foo(NULL); // 编译无法通过
    foo(nullptr);

    return 0;
}
void foo(char *ch) {
    std::cout << "call foo(char*)" << std::endl;
}
void foo(int i) {
    std::cout << "call foo(int)" << std::endl;
}
```

##### 编译线程

```
g++ -std=c++11 t2.c -lpthread
```
t2.c
```
#include <iostream>
#include <thread>
void foo() {
    std::cout << "hello world" << std::endl;
}
int main() {
    std::thread t(foo);
    t.join();
    return 0;
}
```

evpp  安装
```
Install glog
https://github.com/google/glog
./autogen.sh && ./configure && make && make install
cd glog
mkdir build
cd build
cmake ..
make
make install

Install libevent-2.x
git clone https://github.com/libevent/libevent.git
cd libevent
mkdir build
cd build
cmake ..
make
make verify
make install

https://github.com/google/googletest.git
cd googletest
mkdir build
cd build
cmake ..
make
make install

https://github.com/gflags/gflags.git
cd gflags
mkdir build
cd build
cmake ..
make
make Install

https://github.com/Qihoo360/evpp

```
##### gcc 编译出现 internal compiler error: Killed
```
internal compiler error: Killed (program cc1plus)
在 640M 内存的 vps 做编译的时候出现了上述错误.
几经搜索, 才发可能是系统没有交换分区, 编译过程中内存耗尽, 导致了编译中断 …
解决方式也很简单, 就是增加一个交换分区:

1. 创建分区文件, 大小 2G

dd if=/dev/zero of=/swapfile bs=1k count=2048000
2. 生成 swap 文件系统

mkswap /swapfile
3. 激活 swap 文件

swapon /swapfile
这样就木有问题了, 但是这样并不能在系统重启的时候自动挂载交换分区, 这样我们就需要修改 fstab.
修改 /etc/fstab 文件, 新增如下内容:

/swapfile  swap  swap    defaults 0 0
这样每次重启系统的时候就会自动加载 swap 文件了.
```
##### ZeroMQ
http://blog.csdn.net/kaka11/article/details/6652185

C语言程序监控变量的变化
http://blog.csdn.net/pddddd/article/details/46672601

C 语言中 define 的全部使用方法总结
http://blog.jobbole.com/108624/

Nodejs事件引擎libuv源码剖析之：高效线程池(threadpool)的实现
https://www.cnblogs.com/chenyangyao/p/libuv_threadpool.html
https://segmentfault.com/a/1190000005873917
libuv 使用中的一些个人认识
http://blog.csdn.net/wangcg123/article/details/53409918

libuv异步探索
https://windyx.com/blog?id=12
#####libuv 教程
http://luohaha.github.io/Chinese-uvbook/source/threads.html

```
apt-get install curl libcurl3 libcurl3-dev
apt-get install libssh2-1-dev
wget https://www.libssh2.org/download/libssh2-1.8.0.tar.gz
tar xvf *.gx
cd libssh2
./configure
make
make install
```

##### asio libuv对比
https://stackoverflow.com/questions/11423426/how-does-libuv-compare-to-boost-asio
libuv 选型
https://yjhjstz.gitbooks.io/deep-into-node/content/chapter11/chapter11-4.html
libuv 概要及其使用时需要注意的一些问题
https://my.oschina.net/xlqb/blog/389388?p=%7B%7Bpage%7D%7D

事件循环 需求

任何事件，只要是可以监控等待的事件，都可以参与事件循环。

每个事件类型，有一个独立的loop，用不同的线程进行监控。所有的监控，都必须是在收到结果后，再触发回调。

任何事件，都可以注册多个回调函数。

有了事件后，调用相应的 callback进行处理。可以同步，也可以异步。


```
event1.cb1
event1.cb2
event1.cb3
event1.loop.add(event1.cb1)
event1.loop.add(event1.cb2)
event1.loop.add(event1.cb3)
event1.watch()
event1.dispatch()
event1.run(event1.watch(buf),event1.dispatch(buf))
event2.run()
event3.run()

chan1(event1.cb1,event2.cb3,event5,cb4)
chan2(event1.cb2,event1.cb3)
// read or write

每个IE页面一个websockets连接
后台，每个websockets连接一个IOLOOP线程接收页面请求，
这个线程根据不同的请求，发给worker线程工作。
这些worker把相应的结果，返给（某个线程？） 前端相应的页面。

这些是轻量的。



```
##### epoll
https://www.cnblogs.com/lojunren/p/3856290.html
http://blog.chinaunix.net/uid-28541347-id-4273856.html
https://www.cnblogs.com/melons/p/5791788.html
https://www.cnblogs.com/jiji262/archive/2012/02/02/2335484.html
https://www.cnblogs.com/Anker/archive/2013/08/17/3263780.html
http://blog.csdn.net/wangcg123/article/details/54928366
epoll详解
http://blog.csdn.net/majianfei1023/article/details/45772269

##### 有那些好的github上c/c++学习项目？
https://www.zhihu.com/search?type=content&q=c%2B%2B%E5%AD%A6%E4%B9%A0%E9%A1%B9%E7%9B%AE

#####盘点·GitHub最著名的20个Python机器学习项目
https://zhuanlan.zhihu.com/p/31794582

##### C++11 并发指南一(C++11 多线程初探)
http://www.cnblogs.com/haippy/p/3235560.html

##### 漫谈c++11 Thread库之使写多线程程序
http://www.cnblogs.com/ittinybird/p/4820142.html

##### 参考cppreference.com
http://zh.cppreference.com/w/cpp/thread/thread

（不要）使用std::thread
http://www.ituring.com.cn/article/17979

#### C++14特性下的多线程
http://blog.csdn.net/xiaonaiquan/article/details/77825256

##### How to create a self-signed SSL Certificate ...
ihttps://www.akadia.com/services/ssh_test_certificate.html

#### RPC
https://doc.zeroc.com/display/Ice37/Using+the+Linux+Binary+Distributions

C++ 模板元编程的应用有哪些，意义是什么？
https://www.zhihu.com/question/21656266

什么是图灵完备？
https://www.zhihu.com/question/20115374

##### C++11 std::bind std::function 高级用法
http://blog.csdn.net/eclipser1987/article/details/24406203


http://www.cplusplus.com/reference/set/set/


##### STL accumulate计算自定义结构类型
http://blog.csdn.net/cnnumen/article/details/5717629

#####【C++ STL应用与实现】86: 如何使用std::accumulate
http://lib.csdn.net/article/cplusplus/22795

##### elloop的博客值得读
http://my.csdn.net/elloop
http://elloop.github.io/
http://elloop.github.io/categories.html#c++-ref

C++运算符重载详解
http://blog.csdn.net/lishuzhai/article/details/50781753

C++重载运算符（一）如何重载运算符
http://blog.csdn.net/lishuzhai/article/details/50764312

##### 利用C++11的function和bind简化类创建线程
https://www.cnblogs.com/monotone/p/4366170.html

空明流转的博客
https://www.cnblogs.com/lingjingqiu/

λ-calculus（惊愕到手了欧耶，GetBlogPostIds.aspx）
http://www.cppblog.com/vczh/archive/2009/04/08/79291.html

vczh专业造轮子，拉黑抢前排
https://www.zhihu.com/people/excited-vczh/activities

空明流转少年低俗，青年猥琐，中年油腻。
https://www.zhihu.com/people/wuye9036/activities

https://gcc.godbolt.org/

https://hackr.io/tutorials/learn-c-plus-plus


GCC系列: __attribute__((visibility("")))
http://blog.csdn.net/veryitman/article/details/46756683

C++构造函数后面的冒号
http://blog.csdn.net/kaixinbingju/article/details/9094289

c++ 11学习笔记--Lambda 表达式（对比测试Lambda ，bind，Function Object）
https://www.cnblogs.com/budaixi/p/3874011.html


C++11 function使用
http://blog.csdn.net/hanbingfengying/article/details/28651507

旨在搜集国内外各种 C++11 的学习资源
https://github.com/sib9/cpp1x-study-resource

std::vector的几种遍历方式比较
http://blog.csdn.net/ls306196689/article/details/35787955


lambda函数的引入为STL的使用提供了极大的方便。比如下面这个例子，当你想便利一个vector的时候，原来你得这么写：
```
[cpp] view plaincopy
 
vector<int> v;  
v.push_back( 1 );  
v.push_back( 2 );  
//...  
for ( auto itr = v.begin(), end = v.end(); itr != end; itr++ )  
{  
    cout << *itr;  
}  
```
现在有了lambda函数你就可以这么写
```
[cpp] view plaincopy
 
vector<int> v;  
v.push_back( 1 );  
v.push_back( 2 );  
//...  
for_each( v.begin(), v.end(), [] (int val)  
{  
    cout << val;  
} );
```  
而且这么写了之后执行效率反而提高了。因为编译器有可能使用”循环展开“来加速执行过程（计算机系统结构课程中学的）。

##### std::function vs template
https://stackoverflow.com/questions/14677997/stdfunction-vs-template

```
#include <iostream>
#include <functional>
#include <string>
#include <chrono>

template <typename F>
float calc1(F f) { return -1.0f * f(3.3f) + 666.0f; }

float calc2(std::function<float(float)> f) { return -1.0f * f(3.3f) + 666.0f; }

int main() {
    using namespace std::chrono;

    const auto tp1 = system_clock::now();
    for (int i = 0; i < 1e8; ++i) {
        calc1([](float arg){ return arg * 0.5f; });
    }
    const auto tp2 = high_resolution_clock::now();

    const auto d = duration_cast<milliseconds>(tp2 - tp1);  
    std::cout << d.count() << std::endl;
    return 0;
}
```

C++11模版元编程
https://www.cnblogs.com/qicosmos/p/4480460.html

使用C++11变长参数模板 处理任意长度、类型之参数实例
http://blog.csdn.net/yanxiangtianji/article/details/21045525
泛化之美--C++11可变模版参数的妙用
https://www.cnblogs.com/qicosmos/p/4325949.html

模板
http://www.jb51.net/article/41627.htm

https://www.zhihu.com/question/21656266


一个demo学会c++编程
http://blog.csdn.net/luanpeng825485697/article/details/76537402


#### uWS 开始了

```
/home/riddle/source/uWebSockets/tests
g++ -std=c++11 -O3 -I ../src -fPIC -o main main.cpp -luWS -lssl -lz -lpthread
```

```
qmake uWebSockets.pro
成生makefile
```



使用 Prism.js 实现漂亮的代码语法高亮
http://prismjs.com/examples.html
https://highlightjs.org/static/demo/
https://github.com/isagalaev/highlight.js

代码高亮javascript 插件 syntaxhighlighter 使用介绍
http://blog.csdn.net/huutu/article/details/50371460

使用hexo+github搭建免费个人博客详细教程
http://blog.haoji.me/build-blog-website-by-hexo-github.html?from=xa

http://ijiaober.github.io/2014/08/04/hexo/hexo-03/
