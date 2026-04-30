# Сетап: [НАЗВАНИЕ] — App Promotion (Manual)
# Скопируй этот файл, переименуй (напр. app_myapp_us_v1.md) и заполни поля.

---

## Мета-информация

```yaml
type: APP
app_name: "MyApp"                   # Короткое имя приложения
platform: ANDROID                   # ANDROID | IOS
app_id: "com.example.myapp"         # Bundle ID (Android) или Apple App ID (iOS)
                                    # Берётся из Event Manager TikTok после подключения
status: DRAFT                       # DRAFT = залить на паузе | ACTIVE = залить активным
version: 1
```

---

## Нейминг

```yaml
naming:
  campaign: ""                      # Пользователь сообщает перед заливом
  sub_param: "sub7"                 # Имя суб-параметра: "sub7" или "sub_id_3"
  sub_base: ""                      # Базовое значение суб (напр. "avfrites")
                                    # Адсеты будут: avfrites1, avfrites2 ... avfrites5
```

# Трекинговая ссылка для App кампаний НЕ нужна.
# Трекинг идёт автоматически через AppsFlyer / Adjust благодаря:
#   1. Подключению приложения в TikTok Event Manager
#   2. Нейминг кампании содержит суб-параметр (sub7=avfrites) — по нему
#      партнёрская сеть атрибутирует конверсии

---

## Папка с креативами

```yaml
creatives:
  folder: "creatives/[НАЗВАНИЕ_СЕТАПА]/"   # Путь к папке с видео-файлами
                                            # Пользователь сам добавляет видео в эту папку
  ad_text:
    - "Play Now"
    - "Start Play"
  call_to_action:                   # 2-3 кнопки на выбор агента
    - DOWNLOAD                      # Скачать
    - INSTALL_NOW                   # Установить
    - APP_STORE                     # App Store (для iOS)
    - GOOGLE_PLAY                   # Google Play (для Android)
```

---

## Цели для оптимизатора

```yaml
optimizer_targets:
  target_cpa: 0                     # Заполнить: целевая стоимость события PURCHASE в USD
```
