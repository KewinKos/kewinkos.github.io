# Документація API синхронізації знижок

## Ендпоїнти

### 1. Отримання JWT токена
- **Метод:** `POST`
- **URL:** `{{url}}/api/sync/auth/login`
- **Тіло запиту (JSON):**
  ```json
  {
    "email": "testapi@test.com",
    "password": "somesecret"
  }
  ```
- **Опис:**  
  Використовується для аутентифікації. Повертає JWT токен для доступу до інших ендпоїнтів.

---

### 2. Оновлення JWT токена
- **Метод:** `POST`
- **URL:** `{{url}}/api/sync/auth/refresh`
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Опис:**  
  Генерує новий JWT токен на основі поточного (якщо він ще дійсний).
  
---

### 3. Створення знижки
- **Метод:** `POST`
- **URL:** `{{url}}/api/sync/discount/create`
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Тіло запиту (JSON):**  
  Див. [приклад у файлі колекції](https://github.com/KewinKos/kewinkos.github.io/blob/main/Sync%20API.postman_collection.json) (поля `start_date`, `end_date`, `addresses` - необов'язково, переклади, `offers` тощо).
- **Опис:**  
  Створює нову знижку з акційними пропозиціями для вказаних адрес.

---

### 4. Створення знижки (без акційних пропозицій)
- **Метод:** `POST`
- **URL:** `{{url}}/api/sync/discount/create`
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Тіло запиту (JSON):**  
  Див. [приклад у файлі колекції](https://github.com/KewinKos/kewinkos.github.io/blob/main/Sync%20API.postman_collection.json) (поля `start_date`, `end_date`, `addresses` - необов'язково, переклади).
- **Опис:**  
  Створює нову знижку. Знижка має сттаус неактивної до моменту додавання акційних пропозицій

---

### 5. Додавання акційних пропозицій до знижки
- **Метод:** `POST`
- **URL:** `{{url}}/api/sync/discount/{external_id}/add-offers`
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Тіло запиту (JSON):**  
  Див. [приклад у файлі колекції](https://github.com/KewinKos/kewinkos.github.io/blob/main/Sync%20API.postman_collection.json) (поле `offers`).
- **Опис:**  
  Додає акційні пропозиції до знижки за її `external_id`

---

### 6. Оновлення знижки
- **Метод:** `POST`
- **URL:** `{{url}}/api/sync/discount/update/{external_id}`  
  (наприклад: `/update/22505`)
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Тіло запиту (JSON):**  
  Аналогічно тілу для створення, але з оновленими даними.
- **Опис:**  
  Оновлює існуючу знижку за її `external_id`.

---

### 7. Оновлення акційної пропозиції
- **Метод:** `POST`
- **URL:** `{{url}}/api/sync/discount/{external_id}/update-offers`  
  (наприклад: `/22505/update-offers`)
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Тіло запиту (JSON):**  
  Аналогічно тілу для додавання акційних пропозицій, але з оновленими даними.
- **Опис:**  
  Оновлює акційні пропзиції для існуючої знижки за її `external_id`.

---

### 8. Видалення знижки
- **Метод:** `DELETE`
- **URL:** `{{url}}/api/sync/discount/remove/{external_id}`  
  (наприклад: `/remove/22505`)
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Опис:**  
  Видаляє знижку та всі пов’язані з нею акційні пропозиції.

---

### 9. Видалення акційної пропозиції зі знижки
- **Метод:** `DELETE`
- **URL:** `{{url}}/api/sync/discount/{external_id}/remove-offers/{offer_id}`  
  (наприклад: `/api/sync/discount/22505/remove-offers/49599`)
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Опис:**  
  Видаляє акційну пропозицію зі знижки за її `external_id` та `offerId`.
  
---

### 10. Отримання списку знижок
- **Метод:** `GET`
- **URL:** `{{url}}/api/sync/discount/list`  
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Тіло запиту (JSON):**  
  Див. [приклад у файлі колекції](https://github.com/KewinKos/kewinkos.github.io/blob/main/Sync%20API.postman_collection.json) (поля `page`, `perPage`).
- **Опис:**  
  Отримує список знижок, вказавши сторінку `page` та кількість результатів на сторінку `perPage`.
  
---

### 11. Отримання списку акційних пропозицій для знижки
- **Метод:** `GET`
- **URL:** `{{url}}/api/sync/discount/{external_id}/offers-list`  
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Тіло запиту (JSON):**  
  Див. [приклад у файлі колекції](https://github.com/KewinKos/kewinkos.github.io/blob/main/Sync%20API.postman_collection.json) (поля `page`, `perPage`).
- **Опис:**  
  Отримує список акційних пропозицій для знижки, вказавши сторінку `page` та кількість результатів (акційних пропозицій) на сторінку `perPage`.
  
---

### 12. Додавання адрес до акційної пропозиції
- **Метод:** `POST`
- **URL:** `{{url}}/api/sync/discount/{discount_external_id}/add-addresses/{offer_external_id}`  
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Тіло запиту (JSON):**  
  Див. [приклад у файлі колекції](https://github.com/KewinKos/kewinkos.github.io/blob/main/Sync%20API.postman_collection.json) (поле `addresses`).
- **Опис:**  
  Додає нові адреси для акційної пропозиції, вказавши масив адрес `addresses` 
  
---

### 13. Видалення адрес з акційної пропозиції
- **Метод:** `DELETE`
- **URL:** `{{url}}/api/sync/discount/{discount_external_id}/remove-addresses/{offer_external_id}`  
- **Заголовок:**  
  `Authorization: Bearer <JWT_TOKEN>`
- **Тіло запиту (JSON):**  
  Див. [приклад у файлі колекції](https://github.com/KewinKos/kewinkos.github.io/blob/main/Sync%20API.postman_collection.json) (поле `addresses`).
- **Опис:**  
  Видаляє адреси для акційної пропозиції, вказавши масив адрес `addresses` 
  
---

## Валідація даних

### Загальні правила для знижки
| Поле          | Тип даних    | Обмеження                                 | Обов'язкове? |
|---------------|--------------|-------------------------------------------|--------------|
| `start_date`  | Рядок        | Формат: `YYYY-MM-DD` (наприклад: 2025-07-01) | Так          |
| `end_date`    | Рядок        | Формат: `YYYY-MM-DD`                      | Так          |
| `external_id` | Рядок        | Довжина: 1-255 символів                   | Так          |
| `addresses`   | Масив об’єктів | Мінімум 1 елемент                         | Ні          |
| `addresses.*.city` | Рядок | Довжина: 2-512 символів                   | Так          |
| `addresses.*.address` | Рядок | Довжина: 2-512 символів          | Так          |

### Переклади (наприклад, `uk`, `ru`)
| Поле          | Тип даних | Обмеження                     | Обов'язкове? |
|---------------|-----------|-------------------------------|--------------|
| `name`        | Рядок     | Максимум 255 символів         | Так          |
| `description` | Рядок     | Максимум 65535 символів       | Ні           |

---

### Правила для акційних пропозицій (`offers`)
| Поле                     | Тип даних    | Обмеження                                 | Обов'язкове? |
|--------------------------|--------------|-------------------------------------------|--------------|
| `image`                  | Рядок (URL)  | Довжина: 20-512 символів                  | Так          |
| `discount`               | Ціле число   | Діапазон: будь-яке ціле число (наприклад: 20) | Ні          |
| `price_before`           | Число        | Діапазон: 0.00 - 999999.99               | Так          |
| `price_after`            | Число        | Діапазон: 0.00 - 999999.99               | Так          |
| `external_id`            | Рядок        | Довжина: 1-255 символів                   | Так          |
| `addresses`              | Масив об’єктів | Мінімум 1 елемент                         | Так          |
| `addresses.*.city`       | Рядок        | Довжина: 2-512 символів                   | Так          |
| `addresses.*.address`    | Рядок        | Довжина: 2-512 символів                   | Так          |
| `weight`                 | Рядок        | Довжина: 1-255 символів                   | Ні           |
| `is_image_has_price`     | Логічне      | `true` або `false`                        | Так          |
| `external_url`           | Рядок (URL)  | Довжина: 1-255 символів                   | Ні           |
| `barcode`                | Число        | Діапазон: 000000 - 9999999999999          | Ні           |
| `start_date` / `end_date`| Рядок        | Формат: `YYYY-MM-DD`                      | Так          |

### Переклади для пропозицій (наприклад, `uk`, `ru`)
| Поле          | Тип даних | Обмеження                     | Обов'язкове? |
|---------------|-----------|-------------------------------|--------------|
| `name`        | Рядок     | Максимум 255 символів         | Так          |
| `description` | Рядок     | Максимум 255 символів         | Ні           |

---

## Приклади помилок валідації
- Неправильний формат дати: `start_date: "2025/07/01"` (має бути `YYYY-MM-DD`).
- Відсутнє обов’язкове поле: `offers` не передано.
- Недопустиме значення: `discount: "20%"` (має бути цілим числом без символів).
- Перевищення довжини: `image` посилання довше 512 символів.

## Приклад JSON
```{
  "start_date": "2025-07-01",
  "end_date": "2025-07-07",
  "external_id": "22505",
  "addresses": [
    {
      "city": "Харків",
      "address": "пр. Героїв Харкова, 256-б"
    },
    {
      "city": "Харків",
      "address": "вул. Тракторобудівників, 57"
    },
    {
      "city": "Полтава",
      "address": "вул. Ковпака, 26"
    },
    {
      "city": "Миколаїв",
      "address": "пр-т Миру, 1/1"
    },
    {
      "city": "Рівне",
      "address": "вул. Кулика і Гудачека, 23"
    },
    {
      "city": "Чернівці",
      "address": "вул. Руська, 248є"
    }
  ],
  "uk": {
    "name": "Тиждень знижок на продукти",
    "description": "Великий вибір акційних товарів за вигідними цінами"
  },
  "ru": {
    "name": "Неделя скидок на продукты",
    "description": "Большой выбор акционных товаров по выгодным ценам"
  },
  "offers": [
    {
      "image": "https://velmart.ua/wp-content/uploads/2025/03/TT_03.03-09.03_site_VM_.webp",
      "discount": 20,
      "external_id": "556",
      "price_before": 150.00,
      "price_after": 120.00,
      "addresses": [
        {
          "city": "Харків",
          "address": "пр. Героїв Харкова, 256-б"
        },
        {
          "city": "Харків",
          "address": "вул. Тракторобудівників, 57"
        }
      ],
      "weight": "1кг",
      "is_image_has_price": false,
      "external_url": "https://velmart.ua/product-of-week/stegno-kuryache-oholodzhene-1-kg/",
      "barcode": 1234567890123,
      "start_date": "2025-07-01",
      "end_date": "2025-07-07",
      "uk": {
        "name": "Стегно куряче, охолоджене",
        "description": "Свіже м'ясо за вигідною ціною"
      },
      "ru": {
        "name": "Бедро куриное, охлажденное",
        "description": "Свежая курятина по выгодной цене"
      }
    },
    {
      "image": "https://velmart.ua/wp-content/uploads/2025/03/TT_03.03-09.03_site_VM_3.webp",
      "discount": 18,
      "external_id": "557",
      "price_before": 350.00,
      "price_after": 287.00,
      "addresses": [
        {
          "city": "Полтава",
          "address": "вул. Ковпака, 26"
        },
        {
          "city": "Миколаїв",
          "address": "пр-т Миру, 1/1"
        }
      ],
      "weight": "1кг",
      "is_image_has_price": false,
      "external_url": "https://velmart.ua/product-of-week/krevetky-syri-v-pantsyri-rozmorozheni-1-kg/",
      "barcode": 1112223334445,
      "start_date": "2025-07-01",
      "end_date": "2025-07-07",
      "uk": {
        "name": "Креветки сирі в панцирі",
        "description": "Смачні морепродукти"
      },
      "ru": {
        "name": "Креветки сырые в панцире",
        "description": "Вкусные морепродукты"
      }
    },
    {
      "image": "https://velmart.ua/wp-content/uploads/2025/03/TT_03.03-09.03_site_VM_4.webp",
      "discount": 30,
      "external_id": "558",
      "price_before": 50.00,
      "price_after": 35.00,
      "addresses": [
        {
          "city": "Рівне",
          "address": "вул. Кулика і Гудачека, 23"
        },
        {
          "city": "Чернівці",
          "address": "вул. Руська, 248є"
        }
      ],
      "weight": "1кг",
      "is_image_has_price": true,
      "external_url": "https://velmart.ua/product-of-week/apelsyn-1-kg/",
      "barcode": 5678901234567,
      "start_date": "2025-07-01",
      "end_date": "2025-07-07",
      "uk": {
        "name": "Апельсин",
        "description": "Соковиті цитрусові за найкращою ціною"
      },
      "ru": {
        "name": "Апельсин",
        "description": "Сочные цитрусовые по лучшей цене"
      }
    }
  ]
}
