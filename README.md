# yamdb_final
yamdb_final
![Build Status](https://github.com/oborotistova/yamdb_final/workflows/Run%20tests/badge.svg)](https://github.com/oborotistova/yamdb_final/actions/workflows/yamdb_workflow.yml)
## Описание


Проект **YaMDb** собирает **отзывы (Review)** пользователей на **произведения (Titles)**. Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список **категорий (Category)** может быть расширен администратором.
Сами произведения в **YaMDb** не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведению может быть присвоен **жанр (Genre)** из списка предустановленных. Новые жанры может создавать только администратор.
Пользователи оставляют к произведениям текстовые **отзывы (Review)** и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — **рейтинг** (целое число). На одно произведение пользователь может оставить только один отзыв.


## Пользовательские роли

- **Аноним** — может просматривать описания произведений, читать отзывы и комментарии.
- **Аутентифицированный пользователь (user)** — может, как и **Аноним**, читать всё, дополнительно он может публиковать отзывы и ставить оценку произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы; может редактировать и удалять **свои** отзывы и комментарии. Эта роль присваивается по умолчанию каждому новому пользователю.
- **Модератор (moderator)** — те же права, что и у **Аутентифицированного пользователя** плюс право удалять **любые** отзывы и комментарии.
- **Администратор (admin)** — полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.
- **Суперюзер Django** — обладет правами администратора (admin)


## Установка:

### 1. Клонировать репозиторий в рабочую директорию на компьютере:

```bash
git clone git@github.com:Oborotistova/infra_sp2.git
```
или

```bash
git clone https://github.com/Oborotistova/infra_sp2.git
```

### 2. Перейти в директорию infra_sp2/infra:

```bash
cd infra_sp2/infra
```
### 3. Выполнить команду:
```bash
docker-compose up -d
```

### 4. Выполнить миграции:
```bash
docker-compose exec web python manage.py migrate
```

### 5. Создать суперпользователя:
```bash
docker-compose exec web python manage.py createsuperuser
```

### 6. Собрать статику:
```bash
docker-compose exec web python manage.py collectstatic --no-input
```

### 7. Kомандa для заполнения базы данными:
```bash
cat fixtures.json | docker-compose exec -T web python manage.py loaddata --format=json -
```

## Шаблон наполнения env-файла
```
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД
```