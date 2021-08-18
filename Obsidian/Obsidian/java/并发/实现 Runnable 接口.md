# 实现 Runnable 接口
+ 需要实现接口中的 run() 方法。

  ```java
  //{{c1::
  public class MyRunnable implements Runnable {
    @Override
      public void run() {
        // ...
      }
  }
  //}}
  ```

+ 使用 Runnable 实例再创建一个 Thread 实例，然后调用 Thread 实例的 start() 方法来启动线程。

  ```java
  //{{c1::
  }}
  public static void main(String[] args) {
      MyRunnable instance = new MyRunnable();
      Thread thread = new Thread(instance);
      thread.start();
  }
  //}}
  ```
[//anki]: # "java_se_20200604111131321"