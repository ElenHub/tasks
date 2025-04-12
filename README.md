# SPA-приложение "Список задач"

## Описание
Это небольшое SPA-приложение на Vue.js, которое загружает список задач из файла `tasks.json` и позволяет отмечать их как выполненные. Состояние задач сохраняется в локальное хранилище браузера, чтобы при перезагрузке страницы задачи не терялись.

## Установка и запуск

1. Клонируйте репозиторий:
    git clone https://github.com/ElenHub/tasks.git

2. Перейдите в директорию проекта:
    cd tasks-app

3. Установите зависимости:
    npm install

4. Запустите проект:
    npm run server

5. Перейдите в браузер по адресу [http://localhost:8080](http://localhost:8080).

## Задачи
- Загружаются из `tasks.json`.
- Состояние задач сохраняется в `localStorage`.
