# Graceful exit

Представим, что нам надо закрыть программу, но перед этим надо освободить ресурсы итд.

Для этого мы создадим класс `GracefulKiller`, в котором будем перехватывать сигналы `signal.SIGINT` и `signal.SIGTERM`, а также обернем главный цикл в главном треде программы в `try...except` конструкцию, которая ловит исключение `SystemExit` и, если поймала, вызывает `GracefulKiller.kill()`. Таким образом из любого места программы можно будет вызвать `sys.exit()` и ожидать, что программа завершится корректно.

## Код:
```python
import signal
import sys
from itertools import count
from threading import Thread
from time import sleep


class GracefulKiller:
    kill_requested = False

    def __init__(self):
        signal.signal(signal.SIGINT, self.kill)
        signal.signal(signal.SIGTERM, self.kill)

    def kill(self, *args):
        self.kill_requested = True


killer = GracefulKiller()


def computation():
    print(f"computation start")
    for i in count():
        print(f"#{i} computation step")
        sleep(1)
        if killer.kill_requested:
            break
    print(f"computation end")


Thread(target=computation).start()


def loop():
    sleep(3)
    sys.exit()


try:
    print("main loop start")
    loop()
except SystemExit:
    killer.kill()
finally:
    print("main loop end")

```