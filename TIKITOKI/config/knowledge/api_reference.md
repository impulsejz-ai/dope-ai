# TikTok Ads API — Быстрый справочник

Список MCP-инструментов и их параметры. Все инструменты из `meta-ads-mcp` с префиксом `tt_`.

---

## Кампании

### `tt_create_campaign`
```json
{
  "advertiser_id": "7XXXXXXXXXXXXXXXXXX",
  "params": {
    "campaign_name": "TT_MYAPP_20250501_avfrites",
    "objective_type": "APP_PROMOTION",
    "campaign_type": "REGULAR_CAMPAIGN",
    "budget_optimize_on": false,

    // Только для iOS:
    "ios14_quota_type": "SLOT",
    "campaign_app_profile_page_state": "OFF",
    "app_attribution_type": "NON_SKAN"
  }
}
```

### `tt_list_entities` (кампании)
```json
{
  "advertiser_id": "...",
  "entity_type": "campaign",
  "status_filter": "ENABLE"   // ENABLE | DISABLE | ALL
}
```

### `tt_bulk_update_status`
```json
{
  "advertiser_id": "...",
  "entity_type": "campaign",   // campaign | adgroup | ad
  "entity_ids": ["123", "456"],
  "status": "DISABLE"          // ENABLE | DISABLE | DELETE
}
```

---

## Группы объявлений (AdGroups)

### `tt_create_ad_group`
```json
{
  "advertiser_id": "...",
  "params": {
    "adgroup_name": "avfrites1",
    "campaign_id": "7XXXXXXXXXXXXXXXXXX",

    // Приложение (только Android):
    "promotion_type": "APP_ANDROID",
    "app_id": "com.example.myapp",
    // iOS: "promotion_type": "APP_IOS" — app_id НЕ передавать

    // Плейсмент — ТОЛЬКО TikTok:
    "placement_type": "PLACEMENT_TYPE_NORMAL",
    "placements": ["PLACEMENT_TIKTOK"],

    // Оптимизация — стандарт покупка:
    "optimization_goal": "IN_APP_EVENT",
    "conversion_event_code": "PURCHASE",
    // Альтернативы: "INSTALL" (optimization_goal: "INSTALL"), "REGISTRATION"

    // Ставка — всегда авто:
    "bid_type": "BID_TYPE_NO_BID",

    // Бюджет на адсете:
    "budget_mode": "BUDGET_MODE_DAY",
    "budget": 25.00,

    // Гео (ID через tt_search_locations):
    "location_ids": ["6252001"],   // US = 6252001

    // Возраст и пол (стандарт):
    "age_groups": ["AGE_18_24", "AGE_25_34", "AGE_35_44", "AGE_45_54", "AGE_55_100"],
    "gender": [],   // пустой = оба пола

    // Расписание:
    "schedule_type": "SCHEDULE_START_END",
    "schedule_start_time": "2025-05-02 03:01:00",   // 6:01 МСК = 03:01 UTC

    // Трекинг:
    "click_tracking_url": "https://app.adjust.com/abc?sub7=avfrites1&clickid={CLICKID}"
  }
}
```

---

## Объявления (Ads)

### `tt_create_ad`
```json
{
  "advertiser_id": "...",
  "params": {
    "adgroup_id": "7XXXXXXXXXXXXXXXXXX",

    // Умные креативы:
    "creative_material_mode": "SMART_CREATIVE",

    // Персональный профиль (Spark Ads выключен):
  // Профиль должен называться так же как приложение.
  // Найти: TikTok Ads Manager → Инструменты → Профили TikTok
  // Если нет — создать новый с именем приложения там же.
    "identity_type": "CUSTOMIZED_USER",
    "identity_id": "ID_профиля",

    "creative_list": [
      {
        "ad_name": "TT_MYAPP_20250501_V1",
        "ad_format": "SINGLE_VIDEO",
        "video_id": "v09044g40000XXXXXXXXXX",
        "ad_text": "Play Now",
        "call_to_action_id": "DOWNLOAD"
        // Также: "INSTALL_NOW", "GOOGLE_PLAY", "APP_STORE"
      }
    ]
  }
}
```

---

## Аналитика

### `tt_get_insights`
```json
{
  "advertiser_id": "...",
  "report_type": "BASIC",
  "dimensions": ["campaign_id"],   // adgroup_id | ad_id
  "metrics": [
    "spend", "impressions", "clicks", "ctr", "cpc", "cpm",
    "conversion", "cost_per_conversion", "conversion_rate",
    "result", "cost_per_result",
    "app_install", "cost_per_app_install"
  ],
  "start_date": "2025-05-01",
  "end_date": "2025-05-07"
}
```

---

## Поиск гео, интересов, поведений

### `tt_search_locations`
```json
{ "query": "United States", "level": "COUNTRY" }
// level: COUNTRY | PROVINCE | CITY | COUNTY | DMA
```

### `tt_search_interests`
```json
{ "query": "gaming" }
```

### `tt_search_behaviors`
```json
{ "query": "mobile games" }
```

---

## Ресурсы кабинета

### `tt_list_apps`
```json
{ "advertiser_id": "..." }
// Возвращает список приложений с tiktok_app_id и событиями
```

### `tt_list_creative_assets`
```json
{
  "advertiser_id": "...",
  "asset_type": "VIDEO"   // VIDEO | IMAGE
}
// Возвращает video_id для использования в объявлениях
```

### `tt_get_account_info`
```json
{ "advertiser_id": "..." }
// Статус, баланс, валюта, timezone кабинета
```

---

## Валидация

### `tt_validate_campaign_payload`
```json
{
  "payload": {
    "campaign": { ... },
    "ad_group": { ... },
    "ad": { ... }
  }
}
```

### `tt_get_campaign_structure`
```json
{ "section": "all" }
// section: all | campaign | ad_group | ad | enums
// Возвращает полную схему с допустимыми значениями полей
```

---

## Коды гео (часто используемые)

| Страна | location_id |
|--------|------------|
| USA | 6252001 |
| UK | 2635167 |
| Canada | 6251999 |
| Australia | 2077456 |
| Germany | 2921044 |
| France | 3017382 |
| Brazil | 3469034 |
| India | 1269750 |
| Russia | 2017370 |

Точные ID всегда проверяй через `tt_search_locations`.

---

## Лимиты API

- 1000 запросов / час / приложение
- 10 параллельных запросов максимум
- При ошибке 429 — ждать 60 секунд, ретрай (макс 2 раза)
