# Operation-Systems-Voronezh-State-University-Lab-3
Operation Systems
# Это дз по курсу Операционных систем
# Соколов Пётр 4 группа Информатика и выч техника 2 курс 
## Первая программа (receiver.py):
```c
import os
import signal
import sys

# Функция для обработки сигналов
def signal_handler(signum, frame):
    global message
    if signum == signal.SIGUSR1:
        message = "Received SIGUSR1"
    elif signum == signal.SIGUSR2:
        message = "Received SIGUSR2"
    print(message)

# Начальное сообщение
message = "Initial Message"
print(message)

# Установка обработчика сигналов
signal.signal(signal.SIGUSR1, signal_handler)
signal.signal(signal.SIGUSR2, signal_handler)

# Бесконечный цикл
while True:
    # Продолжаем выполнение, ожидая сигналов
    signal.pause()
```
## Вторая программа (sender.py):
```c
import os
import signal
import sys

# Получение PID другого процесса из аргументов командной строки
if len(sys.argv) != 3:
    print("Usage: python sender.py [pid] [signal]")
    sys.exit(1)

pid = int(sys.argv[1])
signal_type = sys.argv[2]

# Отправка сигнала второму процессу
if signal_type == "SIGUSR1":
    os.kill(pid, signal.SIGUSR1)
elif signal_type == "SIGUSR2":
    os.kill(pid, signal.SIGUSR2)
else:
    print("Invalid signal type")
    sys.exit(1)
```

