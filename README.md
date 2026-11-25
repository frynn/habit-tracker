# 📝 Habit Tracker (HabitTrackerProject)

Полнофункциональное веб-приложение для трекинга привычек. Проект разделен на две части: клиентскую (Frontend) и серверную (Backend).

## 🚀 Стек технологий

**Frontend:**
* **Фреймворк:** React (с использованием React Compiler)
* **Сборщик:** Vite
* **Язык:** TypeScript
* **Стилизация:** Tailwind CSS + `tailwindcss-animate`
* **UI-компоненты:** shadcn/ui (Radix UI)
* **Роутинг:** React Router DOM
* **HTTP-клиент:** Axios

**Backend:**
* **Платформа и язык:** C# / ASP.NET Core (.NET 8.0)
* **База данных:** SQLite
* **ORM:** Entity Framework Core 9
* **Аутентификация и безопасность:** JWT Bearer (`Microsoft.AspNetCore.Authentication.JwtBearer`), хэширование паролей через `BCrypt.Net-Next`
* **Валидация и маппинг:** FluentValidation, AutoMapper
* **Документация API:** Swagger / OpenAPI (`Swashbuckle.AspNetCore`)

## 📦 Требования для запуска
Перед началом работы убедитесь, что у вас установлены:
* [Node.js](https://nodejs.org/) (рекомендуется LTS-версия 20.x или 22.x)
* [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
* Git

---

## 🛠 Установка и запуск

### 1. Запуск серверной части (Backend)
1. Откройте терминал и перейдите в папку с бэкендом (там, где находится файл `.sln` или `.csproj`).
2. Восстановите зависимости и примените миграции базы данных SQLite (если база еще не создана):
   ```bash
   dotnet restore
   dotnet ef database update
   ```
3. Запустите сервер:
   ```bash
   dotnet run
   ```
   Сервер запустится (обычно на `https://localhost:7xxx` или `http://localhost:5xxx`). Документация Swagger будет доступна по адресу `http://localhost:5xxx/swagger`. Запомните порт бэкенда — он понадобится для настройки фронтенда.

### 2. Запуск клиентской части (Frontend)
1. Откройте новое окно терминала и перейдите в папку с фронтендом (`habit-tracker`).
2. Установите зависимости:
   ```bash
   npm install
   ```
3. Запустите dev-сервер Vite:
   ```bash
   npm run dev
   ```
   Приложение будет доступно по адресу, указанному в консоли (обычно `http://localhost:5173`).

---

## 📂 Структура проекта (Frontend)

```text
habit-tracker/
├── src/
│   ├── components/     # Переиспользуемые UI-компоненты (кнопки, инпуты, карточки)
│   │   └── ui/         # Базовые компоненты shadcn/ui
│   ├── pages/          # Страницы приложения (Login, Register, Dashboard и т.д.)
│   ├── lib/            # Вспомогательные функции (утилиты, axios-клиенты)
│   ├── hooks/          # Кастомные React-хуки
│   ├── App.tsx         # Корневой компонент с роутингом
│   ├── main.tsx        # Точка входа в приложение
│   └── index.css       # Глобальные стили и переменные Tailwind
├── package.json
├── vite.config.ts
└── tailwind.config.js
```

---

## ⚠️ Решение частых проблем (Troubleshooting)

Если вы столкнулись с ошибками при первом запуске, проверьте следующие пункты:

### 1. Ошибка `npm warn install-scripts ... install scripts blocked`
В новых версиях npm (11+) скрипты установки некоторых пакетов блокируются в целях безопасности. Это ломает работу `esbuild` (критически важный для Vite).  
**Решение:** Разрешите установку скриптов командой:
```bash
npm install-scripts approve esbuild @parcel/watcher
```
Затем удалите `node_modules` и `package-lock.json`, и выполните `npm install` заново.

### 2. Ошибка `Cannot find module ... vite.js` или странные проблемы с путями
Убедитесь, что в полном пути к папке проекта нет символа амперсанда (`&`) или других спецсимволов (например, `D:\Habit tracker Front&Back\` — вызовет ошибку).  
**Решение:** Переименуйте папки так, чтобы путь выглядел как `D:\HabitTrackerProject\habit-tracker`.

### 3. Проблемы с CORS (Ошибка запросов к API)
Если фронтенд не может достучаться до бэкенда, убедитесь, что в настройках C# (в `Program.cs`) разрешен запрос с порта Vite (`http://localhost:5173`).

### 4. Устаревшие данные браузеров
Если в консоли висит предупреждение `[baseline-browser-mapping] The data in this module is over two months old`, просто обновите пакет:
```bash
npm i baseline-browser-mapping@latest -D
```

---

## 📄 Лицензия
Этот проект распространяется под лицензией MIT. Подробности смотрите в файле `LICENSE` (если он есть).
