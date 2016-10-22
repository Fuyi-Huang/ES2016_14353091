###lab4实验报告

----------

1.下面是运行的java代码：

``` java
//Deadlock
class A{
    synchronized void methodA(B b){
        b.last();
    }
    
    synchronized void last(){
        System.out.println("Inside A.last()");
    }
}

class B{
    synchronized void methodB(A a){
        a.last();
    }
    
    synchronized void last(){
        System.out.println("Inside B.last()");
    }
}

class Deadlock implements Runnable{
    A a = new A();
    B b = new B();

    Deadlock(){
        Thread t = new Thread(this);
        int count = 20000;
        
        t.start();
        while(count-- > 0);
        a.methodA(b);
    }

    public void run(){
        b.methodB(a);
    }

    public static void main(String args[]){
        new Deadlock();
    }
}
```
2.下面是linux的bash文件：
``` bash
#!/bin/bash
for(( c=1; c < 1000; c++))
do
	echo "$c times"
	java Deadlock
done
```
3.ubuntu终端的执行命令：
![a](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/lab4/terminal.png?raw=true)

4.执行结果：
![a](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/lab4/Deadlock.png?raw=true)
在第890次循环时产生了死锁

5.死锁的4个必要条件：
- 资源互斥：一个资源每次只能被一个线程占有
- 非抢占：线程拥有的资源只能由线程自愿的释放，不能被其他线程抢占
- 占有且等待：一个进程因请求资源而阻塞时，对已获得的资源保持不放
- 循环等待：若干进程之间形成一种头尾相接的循环等待资源关系

6.产生死锁的原因：
首先A和B类的方法都定义为synchronized，而当一个线程访问object的一个synchronized同步代码块或同步方法时，其他线程对object中所有其它synchronized同步代码块或同步方法的访问将被阻塞。
``` java
 Deadlock(){
        Thread t = new Thread(this);
        int count = 20000;

		t.start();
        while(count-- > 0);
        a.methodA(b);
    }

    public void run(){
        b.methodB(a);
    }
```
上述代码中如果t.start()的线程没有执行完a.methodA(b)，刚刚执行到a.methodA(b)函数里面但是还没有执行b.last()这个函数，即还没有拥有B类的资源就切换了线程。执行run()函数，b.methodB(a)一执行就会占有B类的资源，然后它去调用a.last()请求A类的资源但是发现A类的资源被占有了，所以被阻塞了，然后没办法回到Deadlock()接着执行a.methodA(b)去调用b.last()，然后发现B类的资源也被占有了，所以没办法该线程也被阻塞了，然后就死锁了。