# Сетап: [НАЗВАНИЕ] — Website Traffic (Manual)
# Скопируй этот файл, переименуй (напр. web_offer_us_v1.md) и заполни поля.

---

## Мета-информация

```yaml
type: WEBSITE
offer_name: "MyOffer"               # Короткое имя оффера (используется в нейминге)
status: DRAFT                       # DRAFT = залить на паузе | ACTIVE = залить активным
version: 1
```

---

## Нейминг

```yaml
naming:
  campaign: ""                      # Пользователь сообщает перед заливом
  sub_param: "sub7"                 # Имя суб-параметра: "sub7" или "sub_id_3"
  sub_base: ""                      # Базовое значение (напр. "rocketavtoza")
                                    # Адсеты: rocketavtoza1, rocketavtoza2 ... rocketavtoza5
```

---

## Трекинговая ссылка / Лендинг

```yaml
tracking:
  # {SUB_VALUE} = sub_base + номер адсета (rocketavtoza1, rocketavtoza2...)
  # {DATE} = YYYYMMDD
  landing_url: "https://example.com/lp?{SUB_PARAM}={SUB_VALUE}&clickid={CLICKID}"
  # Пример с трекером:
  # landing_url: "https://go.example.com/click?offer=123&{SUB_PARAM}={SUB_VALUE}&sub2={DATE}"
  impression_url: ""
```

---

## Папка с креативами

```yaml
creatives:
  folder: "creatives/[НАЗВАНИЕ_СЕТАПА]/"
  ad_text:
    - "Play Now"
    - "Start Play"
  call_to_action:
    - LEARN_MORE                    # Подробнее
    - SHOP_NOW                      # Купить
    - SIGN_UP                       # Зарегистрироваться
    - GET_NOW                       # Получить
```

---

## Цели для оптимизатора

```yaml
optimizer_targets:
  target_cpc: 0.50                  # Целевая стоимость клика (CPC) в USD
  target_cpa: 0                     # Целевая стоимость конверсии (0 = не используется)
```
