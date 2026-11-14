# Часть 1 - запуск вручную

Создание и запуск контейнера  redis
<img width="908" height="302" alt="{3BA562B1-FA04-4E09-AF5E-0CF77D30445E}" src="https://github.com/user-attachments/assets/4944191b-2029-45b8-8c94-70e6b224c0e6" />

Проверка работы сайта
<img width="1382" height="936" alt="{5B7A6424-35B3-43F6-B7A6-7C726FF6C6E2}" src="https://github.com/user-attachments/assets/881a6435-70c2-45a9-a798-a81216e2c180" />
<img width="1094" height="234" alt="{F83A42CF-2B4B-40DC-AC9E-764262430D64}" src="https://github.com/user-attachments/assets/7fcec0d8-67be-45a1-9144-f28ee4387a19" />

# Часть 2 - docker-compose.yml

Создаём docker-compose.yml в каталоге /root/rocketcounter 
<img width="624" height="211" alt="{990DC840-649E-41C8-96C5-1F533EED3519}" src="https://github.com/user-attachments/assets/da5bc4f6-2d4f-47ae-a908-ba49a00933c9" />
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
<img width="1640" height="214" alt="{47B4590D-2E04-4DD2-A1D3-64AA03A3E062}" src="https://github.com/user-attachments/assets/d02594b7-9346-4b00-a3d2-6b0a87ed7fb1" />
Проверка сайтов
<img width="1360" height="357" alt="изображение" src="https://github.com/user-attachments/assets/5e71e6fa-5105-401d-b2ae-88d9f7c8de9e" />
<img width="1379" height="415" alt="изображение" src="https://github.com/user-attachments/assets/261f448a-387c-46e9-9c7f-1dc32e73ceaa" />

# Часть 4 - уничтожение стека
Прописываем docker compose down -v
<img width="774" height="195" alt="{6148790E-56B9-4300-BFAF-5DC23234F3AC}" src="https://github.com/user-attachments/assets/5d4af489-9841-48cc-bcb4-87079ebf0d38" />

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
