Title: [Java基础] 多线程
Date: 2013-10-09
Tags: 笔试,面试,Java,基础,编程
Slug: java-basic-thread-IllegalMonitorStateException
Author: Zoey Young
Summary:

笔试中的题目, 考察`wait()`和`notifyAll()`, 还不是很理解

    :::java
    public class Main {
        Integer i = 1;

        public Main() {

        }

        public static void main(String args[]) throws InterruptedException {
            final Main t = new Main();
            synchronized (t.i) {
                Thread thread = new Thread() {
                    public void run() {
                        for (;;) {
                            synchronized (t.i) {
                                System.out.println("a:" + (++t.i));
                                try {
                                    Thread.sleep(100);
                                } catch (InterruptedException e) {
                                    e.printStackTrace();
                                }
                                t.i.notifyAll();
                            }
                        }
                    }
                };
                thread.start();
                t.i.wait();
                System.out.println("b:" + (++t.i));
            }
        }
    }

运行结果:

    a:2
    Exception in thread "Thread-0" java.lang.IllegalMonitorStateException
        at java.lang.Object.notifyAll(Native Method)
        at Main$1.run(Main.java:21)
