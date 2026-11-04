# Jumper

Игра в стиле Doodle Jump для Telegram Mini App. Один файл `index.html`, без сборки и зависимостей.

## Что внутри

- 20 скинов и 10 карт с редкостью (обычные → легендарные), открываются из сундуков за монеты
- Ежедневное колесо бонусов с супер-игрой (монета на каждом островке)
- Усилители: джетпак и прыгалки
- Управление касаниями или наклоном телефона
- Прогресс сохраняется в облаке Telegram (CloudStorage) и в браузере
- Автоматическая экономия графики на слабых телефонах

## Залить на GitHub Pages

1. Создай репозиторий `jumper` на GitHub и загрузи в него `index.html` и `README.md`.
2. Открой **Settings → Pages**.
3. В **Source** выбери `Deploy from a branch`, ветку `main`, папку `/ (root)` и нажми **Save**.
4. Через 1–2 минуты игра будет доступна по адресу:
   `https://rubashinsem.github.io/jumper/`

## Подключить к боту

Кнопка запуска игры (aiogram 3):

```python
from aiogram.types import InlineKeyboardMarkup, InlineKeyboardButton, WebAppInfo

kb = InlineKeyboardMarkup(inline_keyboard=[[
    InlineKeyboardButton(text="🎮 Играть", web_app=WebAppInfo(url="https://rubashinsem.github.io/jumper/"))
]])
await message.answer("Прыгай выше всех!", reply_markup=kb)
```

Ещё можно повесить игру на кнопку меню бота: в @BotFather → `/mybots` → бот → **Bot Settings → Menu Button**, указать тот же URL.

## Настройки баланса

Всё в `index.html`, в блоке `<script>`:

| Что | Где |
|---|---|
| Цена сундука скинов / карт | `ROLL = { skin: 100, map: 500 }` |
| Шансы редкостей в сундуке | `RAR` (поле `w`) |
| Шансы на колесе бонуса | `WHEEL` (поле `w`) |
| Время джетпака / прыгалок | `JET_TIME`, `BOOTS_TIME` |
| Шанс появления усилителей | функция `fill()` |

## Важно

Монеты хранятся на стороне игрока, поэтому их можно накрутить. Пока в игре нет покупок за реальные деньги, это не страшно. Если появятся Telegram Stars или общий рейтинг, баланс нужно перенести на сервер бота.
