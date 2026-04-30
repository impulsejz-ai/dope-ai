# TikTok Ads Mass Upload Agent

Система автоматического массового залива рекламных кампаний в TikTok Ads через Claude Code.

## Что умеет система

- **Массовый залив** — заливает один сетап сразу в несколько рекламных кабинетов за один запрос
- **Мобильные приложения** — кампании на установку iOS/Android приложений
- **Веб-трафик** — кампании на переходы по ссылкам
- **Гибкий таргетинг** — geo/аудитории задаются в сетапе или оставляются пустыми (broad)
- **Отчёты** — статистика по аккаунтам и кампаниям
- **Оптимизация** — пауза слабых, масштаб сильных

## Навыки (Skills)

| Команда | Что делает |
|---------|-----------|
| `/tiktok-agent` | Главный агент, точка входа |
| `/mass-uploader` | Залив сетапа в один или несколько аккаунтов |
| `/account-manager` | Добавить/удалить/проверить рекламный кабинет |
| `/campaign-reporter` | Отчёт по метрикам (день/3 дня/неделя/месяц) |
| `/campaign-optimizer` | Оптимизация: пауза слабых, бюджет сильным |

## Структура папок

```
TIKITOKI/
├── .claude/
│   └── settings.json          # MCP конфиг (токены)
├── skills/                    # Claude Skills
│   ├── tiktok-agent/
│   ├── mass-uploader/
│   ├── account-manager/
│   ├── campaign-reporter/
│   └── campaign-optimizer/
├── config/
│   ├── accounts.md            # Список рекламных кабинетов
│   ├── naming_rules.md        # Правила нейминга
│   ├── safety_rules.md        # Правила безопасности
│   ├── setups/                # Сетапы для залива
│   │   ├── _template_app.md   # Шаблон App Install
│   │   └── _template_web.md   # Шаблон Website Traffic
│   ├── history/               # Лог действий по датам
│   └── knowledge/             # База знаний
└── CLAUDE.md                  # Этот файл
```

## MCP Сервер

Используется `meta-ads-mcp` (AvyanshKatiyar) с 15 TikTok инструментами:
- `tt_create_campaign` / `tt_create_ad_group` / `tt_create_ad`
- `tt_bulk_update_status` — массовое включение/отключение
- `tt_get_insights` — аналитика
- `tt_list_creative_assets` — список видео/картинок
- `tt_list_apps` — список приложений
- `tt_search_locations` / `tt_search_interests` / `tt_search_behaviors`

## Структура кампании в TikTok

```
Advertiser (Кабинет)
└── Campaign (Кампания)
    ├── objective: APP_PROMOTION
    ├── campaign_type: REGULAR_CAMPAIGN (ручная)
    ├── iOS: ios14_quota_type=SLOT, SKAN=OFF, profile_page=OFF
    └── AdGroup × 5 (имена = sub_value1..5)
        ├── promotion_type: APP_ANDROID | APP_IOS | WEBSITE
        ├── placement: PLACEMENT_TIKTOK only
        ├── optimization_goal: IN_APP_EVENT → PURCHASE
        ├── bid_type: BID_TYPE_NO_BID (авто)
        └── Ad (одно объявление, все видео в creative_list)
            ├── creative_material_mode: SMART_CREATIVE
            ├── identity_type: CUSTOMIZED_USER (Spark Ads OFF)
            ├── video_ids[] — все видео из папки
            ├── ad_text: "Play Now" | "Start Play"
            └── call_to_action: DOWNLOAD | INSTALL_NOW | APP_STORE | GOOGLE_PLAY
```

## Быстрый старт

1. Установить uv: `pip install uv` (если не установлен)
2. MCP запускается автоматически через `uvx meta-ads-mcp` (настроен в settings.json)
3. Заполнить `.claude/settings.json` — токен и advertiser_id
3. Добавить кабинеты в `config/accounts.md`
4. Создать сетап в `config/setups/`
5. Запустить `/mass-uploader`

## Важно

- Перед заливом всегда читать `config/safety_rules.md`
- Каждое действие логируется в `config/history/YYYY-MM-DD.md`
- Максимум 1000 запросов к API в час (лимит TikTok)
