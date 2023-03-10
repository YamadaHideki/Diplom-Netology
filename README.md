# Дипломная работа «Облачное хранилище»
Стек: Spring Boot, Spring Security, Spring Data JPA, PostgreSQL, JUnit, Mockito, Maven, Docker.
## Описание
Проект предоставляет собой REST сервис для загрузки, скачивания, переименования, удаления и вывода списка загруженных файлов пользователя. 
Все запросы к сервису авторизованы.
Веб приложение (FRONT) подключается к сервису и использует его функционал для манипуляции с файлами.
## FRONT
Репозиторий FRONTEND приложения доступен по адресу https://github.com/YamadaHideki/Diplom-Netology/netology-diplom-frontend.

FRONTEND отправляет запросы на http://localhost:9090/ который слушает REST приложение.

## BACKEND
Репозиторий BACKEND доступен по адресу https://github.com/YamadaHideki/Diplom-Netology/netology-diplom-backend.

BACKEND слушает порт 9090 на http://localhost. На этот порт посылает запросы FRONTEND приложение.

## Запуск
Для запуска установите Docker, откройте консоль, поставьте путь в консоли тот же, что и папка с проектом.
Введите в консоль команду:
```
docker-compose up --build
```

Для остановки приложения нажать Ctrl+C
## Пример использования
Для авторизации используйте: имя пользователя - `user`, пароль `password`
Загрузите любой файл до 100 мб.
## Взаимодействие приложений
FRONT приложение отправляет credentials в теле запроса на эндпоинт /login BACKEND приложения.
Запрос проходит через CORS filter, CSRF filter, перехватывается JwtTokenFilter и передается далее на аутентификацию.
В случае успешной аутентификации генерируется токен, которые возвращается на FRONT в ответе с заголовком `auth-token`
Все дальнешие запросы FRONT делает с этим токеном в заголовке `auth-token`.
При выходе из приложения вызывается метод BACKEND /logout, который удаляет токен из TokenStore и все дальнейшие запросы с этим токеном не действительны.
