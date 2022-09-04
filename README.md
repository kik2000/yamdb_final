# api_yamdb
![example workflow](https://github.com/kik2000/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
## О проекте

Данный проект является учебным.
Проект YaMDb собирает отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории (Category): «Книги», «Фильмы», «Музыка».
Сами произведения в YaMDb не хранятся.
Произведению может быть присвоен жанр (Genre).
Пользователи YaMDb оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число).
Проект упакован в Docker контейнеры.


## Ключевые функции:

- Работа с категориями (получение, создание, удаление)
- Работа с жанрами (получение, создание, удаление)
- Работа с произведениями (получение, создание, обновление, удаление)
- Работа с ревью (получение, создание, обновление, удаление)
- Работа с комментариями (получение, создание, обновление, удаление)
- Работа с пользователями (получение, создание, обновление, удаление)
- Создание, обновление и проверка JWT authentication токенов пользователей
- Для детального описания функционала API применена библиотека   [Redoc](https://github.com/Redocly/redoc).

## Минимальные требования:

Установка Docker 

Выполните установку docker для вашей операционной системы согласно инструкции на официальном сайте https://docs.docker.com/desktop/

### Ubuntu

- Убедитесь, что ваш ПК соответствует минимальным требованиям:

- 64-битное ядро и CPU с поддержкой виртуализации.

- поддержка KVM виртуализации. Откройте терминал и введите


```commandline
modprobe kvm_intel # для процессоров Intel

```
```commandline
modprove kvm_amd # для процессоров AMD
```
```commandline
sudo apt install curl
```



- скачайте скрипт для установки docker
```commandline
curl -fsSL https://get.docker.com -o get-docker.sh
```

- запустите скрипт
```commandline
sh get-docker.sh
```

- удалите старые версии файлов
```commandline
sudo apt remove docker docker-engine docker.io containerd runc 
```

- обновите список пакетов
```commandline
sudo apt update
```

- установите пакеты для загрузки через https
```commandline
sudo apt install \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg-agent \
  software-properties-common -y 

- добавьте ключ gpg

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

```
- добавьте репозиторий Docker в пакеты
```commandline
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" 
```
- обновите индекс пакетов
```commandline
sudo apt update
```
- установите docker и docker-compose
```commandline
sudo apt install docker docker-compose -y 
```
- проверьте статус установки
```commandline
sudo systemctl status docker 
```
### Запуск проекта на сервере:
1. Сделать fork проекта в свой GitHUB;
```commandline
https://github.com/kik2000/yamdb_final.git
```
2. В разделе проекта Setting/Secrets указать логин и пароль DockerHUB с ключами:
```commandline
DOCKER_USERNAME, DOCKER_PASSWORD
```
3.  В разделе проекта Setting/Secrets указать параметры (хост, логин, ssh-key, пароль ) DockerHUB с ключами:
```commandline
HOST, USER, SSH_KEY, PASSPHRASE
```
4. В разделе проекта Setting/Secrets указать параметры секретного ключа и базы данных:
```commandline
SECRET_KEY, DB_ENGINE, DB_NAME, POSTGRES_USER, POSTGRES_PASSWORD, 
DB_HOST, DB_PORT  
```
5. В разделе проекта Setting/Secrets указать ID телеграм-канала и токен телеграм-бота для получения уведомлений с ключами:
```commandline
TELEGRAM_TO, TELEGRAM_TOKEN
```

- Скопировать файлы docker-compose.yaml и nginx/default.conf из проекта на сервер в home/<ваш_username>/docker-compose.yaml и home/<ваш_username>/nginx/default.conf соответственно.

6. На GitHUB выполнить commit, после которого запустятся процедуры workflow;
7. На сервере выполнить миграции, создать суперюзера, собрать статику:
```commandline
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```
8. Работоспособность приложения можно проверить без развертывания на уже запущенном сервере:

http://178.154.195.243/admin



## Об авторе

Васильев Кирилл