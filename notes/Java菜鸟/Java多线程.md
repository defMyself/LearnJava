# Java多线程

## 0x01线程的生命周期

1. 新建状态：使用new关键字和Thread类或其子类建立一个线程对象后，该线程就属于新建状态。
2. 就绪状态：线程对象调用`start()`方法之后，该线程就进入就绪状态。就绪队列的线程处于就绪队列中，要等待JVM中的线程调度器的调度。
3. 运行状态：就绪状态的线程获取CPU资源，就可以执行`run()`,此时线程便处于运行状态。处于运行状态的线程可以变为阻塞状态，就绪状态和死亡状态。
4. 阻塞状态：线程执行`sleep()`,`suspend()`等方法，失去所占用资源之后，该线程就从运行状态进入阻塞状态。之后还可以重新进入就绪状态。
   1. 等待阻塞：运行状态中的线程执行`wait()`方法，使线程进入到等待阻塞状态。
   2. 同步阻塞：线程在获取`synchronized`同步锁失败(因为同步锁被其他线程占用)。
   3. 其他阻塞：调用线程的`sleep`，或者`join`发出了IO请求时，线程就会进入到阻塞状态。当sleep状态超时，join等待线程终止或超时，IO处理完毕，线程重新转入就绪状态
5. 死亡状态：运行的进程任务完成或因其他原因进入终止状态

## 0x02线程的优先级

每个线程都有一个优先级，Java优先级是1-10的整数

默认优先级为`NORM_PRIORITY` 5

## 创建一个线程

* 实现`Runnable`接口
* 继承`Thread`类本身
* 通过`Callable` 和 `Future`创建线程



```java
class RunnableDemo implements Runnable {
    private Thread t;
    private String threadName;
    
    RunnableDemo(String name) {
        threadName = name;
        System.out.println("Creating " + threadName );
    }
    
    public void run() {
        System.out.println("Running " + threadName);
        try {
            for(int i = 4; i > 0; i--) {
                System.out.println("Thread: " + threadName + ", "  + i);
                Thread.sleep(50);
            }
        }catch (InterruptedException e) {
            System.out.println("Thread " + threadName + " interrupted.");
        }
        System.out.println("Thread " + threadName + " exiting.");
    }
    
    public void start() {
        System.out.println("Starting " + threadName );
        if (t == null) {
            t = new Thread(this, threadName);
            t.start();
        }
    }
}

public class TestThread {
    public static void main(String args[]) {
        RunnableDemo R1 = new RunnableDemo( "Thread-1");
        R1.start();
        
        RunnableDemo R2 = new RunnableDemo( "Thread-2");
        R2.start();
    }
}
```



继承`Thread`类

```java
class ThreadDemo extends Thread {
    private Thread t;
    private String threadName;
    
    ThreadDemo(String name) {
        threadName = name;
        System.out.println("Creating " + threadName);
    }
    
    public void run() {
        System.out.println("Running " + threadName);
        try {
            for(int i=4;i>0; i--) {
                System.out.println("Thread: " + threadName + ", " + i);
                Thread.sleep(50);
            }
        } catch (InterruptedException e) {
            System.out.println("Thread " + threadName + " exiting.");
        }
    }
    
    public void start() {
        System.out.println("Starting " + threadName);
        if (t==null) {
            t = new Thread(this, threadName);
            t.start();
        }
    }
}

public class TestThread {
    public static void main(String args[]) {
        ThreadDemo T1 = new ThreadDemo("Thread-1");
        T1.start();
        
        ThreadDemo T2 = new ThreadDemo("Thread-2");
        T2.start();
    }
}
```



```java
public void start();
public void run();
public final void setName(String name);
public final void setPriority(int priority);
public final void setDaemon(boolean on);
public final void join(long millisec);
public void interrupt();
public final boolean isAlive();

// 静态方法
public static void yield();
public static void sleep(long millisec);
public static boolean holdLock(Object x);
public static Thread currentThread();
public static void dumpStack()
```



Callable和Future



