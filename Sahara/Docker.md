# Docker + Ansible = ❤️

  

### Какие проблемы при классической развертке приложений?

  

- Конфликт версий зависимостей

- Приложение работает на сервер А но не работает на Б

- Не безопасный запуск (конфликт портов, конфликты  зависимости пакетов)

- Невозможность масштабирования

  

### Что дает Docker?

  

- Изолированное окуржение для запуска приложений

- Простое управление и обновление и откат приложений

- Легкое масштабирование приложений под нагрузкой

- Удобный способ доставки приложений

- Простоя работа с сетью и Service Discovery

  

---

  

### Какие проблемы администрирования существуют?

  

- Часто повторяющиеся задачи

- Медленная доставка приложений

- Повторение сложных задач

- Нет единой точки хранения состояния серверов

  

### Что дает Ansible?

  

- Простую автоматизацию сложных и повторяющиеся задач

- Хранение вашей конфигурации как код

- Экономия времени и переносимость решений

- Декларативная система описаний через YML

- Нет необходимости дополнительного ПО на сервере

  

# Установка Ubuntu на VM

  

![Untitled](Docker%20+%20Ansible%20=%20%E2%9D%A4%EF%B8%8F%205faf871167f94f00afd8e044b8a28d68/Untitled.png)

  

1. Скачать [Ubuntu server](https://ubuntu.com/download/server)

2. Сгенерировать ssh ключ приватный и публичный

  

```bash

cd .ssh

ssh-keygen

  

```

  

1. Oracle virtual box

2. Смотрировать диск, установить убунту по дефолту

3. Ставим правила на локальный порт что бы достучаться по шушу

  

![Untitled](Docker%20+%20Ansible%20=%20%E2%9D%A4%EF%B8%8F%205faf871167f94f00afd8e044b8a28d68/Untitled%201.png)

  

Копируем наш публичный ключ **`cat C:\Users\ivan_\.ssh\id_rsa.pub`**

  

Стучимся по шушу на 2222 порт `ssh ancill@127.0.0.1 -p 2222`

  

Прыгаем в `cd ~/.ssh` и `nano authorized_keys` кидаем наш публичный ключ

  

### Basic commands and Utils for Linux

  

```bash

pwd - где сейчас

ls что в директории

ls -l показать в списке

ls -la  показать со скрытыми

mkdir test создать директорию тест

rm package-lock.json удалить файл

rm -R test удалить всю папку

  

cp README.md README2.md копировать

mv README2.md README3.mv переместить

cat README.md показать контент файла

tail -l README.md показать с конца файл

head -l README.md посмотреть начало файла

less README.md посмотреть весь файл

  

чейним команды

grep ищет по файлу и получает строку

cat package.json | grep "jest"

cat package.json | head -1 "jest"

  

find ./apps -name "main.ts" найти в директории файл

echo 1 вывести 1 на экран

echo 1 > a.txt запсать в файл 1

  

diff file  otherFIle  посмотреть отличия в файлах

df посмотреть заполненость диска

  

```

  

- **htop** - Просмотр запущенных процессов в линуксе

    ![Untitled](Docker%20+%20Ansible%20=%20%E2%9D%A4%EF%B8%8F%205faf871167f94f00afd8e044b8a28d68/Untitled%202.png)

  

### Установка Docker

  

Начинаем с ****Install using the repository****

  

[Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

  

Убрать судо из докера

  

[Post-installation steps for Linux | Docker Documentation](https://docs.docker.com/engine/install/linux-postinstall/)

  

### Чем отличается докер от вм?

  

![Untitled](Docker%20+%20Ansible%20=%20%E2%9D%A4%EF%B8%8F%205faf871167f94f00afd8e044b8a28d68/Untitled%203.png)

  

Отсутсвие гостевой ОС главное отличие

  

Контейнер это не вертуальная машина, это изолированый namespace с доп обвязками докера и дополнительный библотеки которые позволяют докеру работать с системой

  

![Untitled](Docker%20+%20Ansible%20=%20%E2%9D%A4%EF%B8%8F%205faf871167f94f00afd8e044b8a28d68/Untitled%204.png)

  

## Управление контейнером

  

![Untitled](Docker%20+%20Ansible%20=%20%E2%9D%A4%EF%B8%8F%205faf871167f94f00afd8e044b8a28d68/Untitled%205.png)

  

`docker ps` просто запущенные контейнеры

  

`docker ps -a` Выводит контейнеры которые были выпущенны

  

`docker rm ‘id’` удаление контейнера

  

`docker pause my-mongo` поставить на паузу

  

`docker unpause my-mongo` возобновить работу

  

`docker run —name my-mongo -d mongo`  запускаем контейнер монги *флаг -d позволяет запустить контейнер отдельно от сессии баша*

  

 `docker kill —signal=1 my-mongo`  убить контейнер который не отвечает

  

`docker container prune`  Почистить контейнеры которые не запущены

  
### **Логи и статистика работы**

  

mongodb - название контейнера

  

`docker stats` будет выводить сколько ресурсов забирает контейнер

  

`docker inspect mongodb` посмотреть детальную информацию по контейнеру

  

`docker inspect -s mongodb` посмотреть сколько места занимает контейнер

  

`docker inspect -f "{{.State.Status}}" mongodb`  посмотреть отдельное свойство в джейсончике

  

`docker logs mongodb`  Посмотреть логи

  

`docker logs mongodb | grep “id”` подсветить оперделенный параметр в логах

  

`docker logs mongodb | grep "11.857"`  подсветить ошибку в логах

  

`docker logs mongodb | grep "id.*" -m 2` вывести все что id и все за ним

  

`docker logs mongodb -f`  следовать за логом в баше

  

`docker logs mongodb > test.txt` вывод логов в файл test.txt

  

Взять из логов все что было выпущенно за 9 утра 26T09:

  

`docker logs mongodb | grep "26T09:" > test-new.txt`

  

`cat test-new.txt`  вывести на экран этот файл

