# Часть 1 - запуск вручную

Создание и запуск контейнера  redis и связка через --link
<img width="1473" height="217" alt="изображение" src="https://github.com/user-attachments/assets/e0dc9344-85f5-4b47-ade8-163eb0ec4db4" />

Проверка работы сайта
<img width="1382" height="936" alt="{5B7A6424-35B3-43F6-B7A6-7C726FF6C6E2}" src="https://github.com/user-attachments/assets/881a6435-70c2-45a9-a798-a81216e2c180" />

http-ответ
<img width="1094" height="234" alt="{F83A42CF-2B4B-40DC-AC9E-764262430D64}" src="https://github.com/user-attachments/assets/7fcec0d8-67be-45a1-9144-f28ee4387a19" />

# Часть 2 - docker-compose.yml

Создаём docker-compose.yml в каталоге /root/rocketcounter 
<img width="712" height="243" alt="изображение" src="https://github.com/user-attachments/assets/a56d493c-0016-4a15-af74-fd94a53fa9c5" />

Заполняем файл
```
services:
  redis:
    image: redis

  rocketcounter:
    image: rotorocloud/rocket-counter
    ports:
      - "8085:5000"
```

Запускаем
<img width="1606" height="194" alt="{AA4EC1AD-BAE3-4411-B8B7-A281A1516293}" src="https://github.com/user-attachments/assets/5dab5d4a-0832-4c49-8ded-38307854441a" />

# Часть 3 - масштабирование
Изменяем docker-compose.yml на
```
services:
  redis:
    image: redis

  rocketcounter:
    image: rotorocloud/rocket-counter
    ports:
      - "0:5000"
```

Запуск
<img width="1711" height="254" alt="{AD627974-8A53-4869-97B0-62FC5F791F58}" src="https://github.com/user-attachments/assets/2d70bbb9-481f-4177-8b99-74e0cc26a4ef" />

Проверка сайтов
<img width="1360" height="357" alt="изображение" src="https://github.com/user-attachments/assets/5e71e6fa-5105-401d-b2ae-88d9f7c8de9e" />
<img width="1379" height="415" alt="изображение" src="https://github.com/user-attachments/assets/261f448a-387c-46e9-9c7f-1dc32e73ceaa" />

# Часть 4 - уничтожение стека
Прописываем docker compose down -v, проверяем 
<img width="1788" height="289" alt="{E52D6803-1277-479E-ACAA-7F64AD4B7782}" src="https://github.com/user-attachments/assets/2d25dd7c-7a9c-4826-b64d-6e5eaf4e6ee5" />

# Вопросы
Q: Зачем в Ч.1 использовался --link и почему в Compose он не нужен?

A: --link связывает контейнеры вручную, в compose контейнеры создаются сразу в одной рользовательской сети

Q: Чем отличается image от build в Compose?

A: image указывает готовый образ, build задаёт параметры сборки образа 

Q: Почему нельзя масштабировать сервис с публикацией фиксированного порта на одном хосте? Перечислите способы обойти это ограничение.

A: Несколько образов не могут одновременно занимать один порт. Контра - динамические порты, диапазоны портов, балансировщик

Q: Что делает docker compose down -v и чем отличается от down без -v?

A: -v удаляет тома

Q: Как в Compose обеспечивается сетевое имя сервиса для обращения из другого сервиса?

A: Compose создаёт отдельную сеть для проекта, где все контейнеры получают DNS-имена
