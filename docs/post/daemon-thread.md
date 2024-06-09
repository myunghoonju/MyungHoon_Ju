#### Daemon thread
```text
데몬 스레드는 낮은 우선순위를 가지고 백그라운드에서 실행  
보통 사용자 작업을 방해하지 않고 백그라운드에서 자동으로 작동되는 기능
ex) 1. ForkJoinPool -> 데몬 스레드를 생성  
    2. main thread(설정없으면) -> 사용자 스레드  
모든 사용자 스레드가 작업을 완료하면 JVM이 강제종료 시킴
```

```text
expected output::  

daemon thread start
daemon thread start
daemon thread start
daemon thread start
daemon thread start

user thread start

main thread end
```

```java
    public static void main(String[] args) throws InterruptedException {
        Thread userThread = new Thread(() -> {
            try {
                Thread.sleep(3000);
                log.info("user thread start");
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        });

        Thread daemonThread = new Thread(() -> {
            while (true) {
                try {
                    Thread.sleep(500);
                    log.info("daemon thread start");
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            }
        });

        daemonThread.setDaemon(true);

        userThread.start();
        daemonThread.start();

        userThread.join();

        log.info("main thread end");
    }
```

```text
expected output::  

user thread daemon? false
is child of user thread daemon? false

is child of daemon thread daemon? true
daemon thread daemon? true

main thread end
```

```java
 public static void main(String[] args) throws InterruptedException {
        Thread userThread = new Thread(() -> {
            new Thread(() -> {
                log.info("is child of user thread daemon? {}", Thread.currentThread().isDaemon());
            }).start();

            log.info("user thread daemon? {}", Thread.currentThread().isDaemon());
        });

        Thread daemonThread = new Thread(() -> {
            new Thread(() -> {
                log.info("is child of daemon thread daemon? {}", Thread.currentThread().isDaemon());
            }).start();
            log.info("daemon thread daemon? {}", Thread.currentThread().isDaemon());
        });

        daemonThread.setDaemon(true);

        userThread.start();
        daemonThread.start();

        userThread.join();

        log.info("main thread end");
    }
```

