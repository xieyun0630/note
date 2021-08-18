# 实现 Callable 接口
+ 与 Runnable 相比，Callable 可以有返回值，返回值通过 `FutureTask` 进行封装。
  ```java
  //{{c1::
  public class MyCallable implements Callable<Integer> {
      public Integer call() {
          return 123;
      }
  }
  //}}
  ```
  
  + 调用

  ```java
  //{{c1::
  public static void main(String[] args) throws ExecutionException, InterruptedException {
      MyCallable mc = new MyCallable();
      FutureTask<Integer> ft = new FutureTask<>(mc);
      Thread thread = new Thread(ft);
      thread.start();
      System.out.println(ft.get());
  //}}
  }
  ```
  
  
  [//anki]: # "java_se_20200604111131323"