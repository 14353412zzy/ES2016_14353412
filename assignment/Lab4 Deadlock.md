#Lab4 Deadlock
###截图：
![enter image description here](https://raw.githubusercontent.com/14353412zzy/ES2016_14353412/master/pictures/Deadlock.png)
###产生死锁的必要条件：
#####①互斥条件：一个资源每次只能被一个进程使用
#####②请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放
#####③不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺
#####④循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系
###上述死锁的解释
首先A和B中的methodX,last都是synchronized；
当一个线程访问object的一个synchronized(this)同步代码块时，其他线程对object中所有其它synchronized(this)同步代码块的访问将被阻塞；
mian线程跑a.methodA(b), 新线程t跑b.methodB(a);
main设置有等待时间count，故存在一种情况，在main运行a.methodA(b)但还没有运行完其中的b.last()时，将资源让给线程t，此时t运行b.methodB(a)的a.last便会被a.methodA阻塞，同时又阻塞了b.last()，因而产生死锁；
