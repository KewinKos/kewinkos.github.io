### Документація до XML-структури "promotions"

Цей XML-документ містить дані про акційні пропозиції. Він складається з кореневого елемента `<promotions>`, що містить один або кілька елементів `<promotion>`.

---

### 1. Кореневий елемент
**`<promotions>`**  
*Контейнер для всіх акцій.*

- Містить один або більше елементів `<promotion>`.

---

### 2. Елемент акції
**`<promotion>`**  
*Описує окрему акцію.*

#### 2.1. Назва акції  
**`<name>`**  
*Назва акції на різних мовах.*  
- **`<uk>`** – українська версія назви (використовує `CDATA`).  
- **`<ru>`** – російська версія назви (використовує `CDATA`).  

#### 2.2. Опис акції  
**`<description>`**  
*Опис акції на різних мовах.*  
- **`<uk>`** – українська версія опису (використовує `CDATA`).  
- **`<ru>`** – російська версія опису (використовує `CDATA`).  

#### 2.3. Ідентифікатор акції  
**`<identifier>`**  
*Унікальний числовий ідентифікатор акції.*

#### 2.4. Дати проведення акції  
- **`<start_date>`** – дата початку акції у форматі `YYYY-MM-DD`.  
- **`<end_date>`** – дата завершення акції у форматі `YYYY-MM-DD`.  

#### 2.5. Адреси проведення акції  
**`<adresses>`**  
*Список міст і магазинів, де діє акція.*  

- **`<item>`** – окремий населений пункт, де діє акція.  
  - **`<id>`** – унікальний ідентифікатор міста.  
  - **`<city>`** – назва міста на різних мовах.  
    - **`<uk>`** – назва міста українською.  
    - **`<ru>`** – назва міста російською.  
  - **`<shops>`** – список магазинів у місті.  
    - **`<shop>`** – окремий магазин.  
      - **`<id>`** – унікальний ідентифікатор магазину.  
      - **`<address>`** – адреса магазину.

---

### 3. Пропозиції акції
**`<offers>`**  
*Список товарів, які беруть участь у акції.*

- **`<offer>`** – окремий товар.  
  - **`<name>`** – назва товару на різних мовах.  
    - **`<uk>`** – українська версія назви (використовує `CDATA`).  
    - **`<ru>`** – російська версія назви (використовує `CDATA`).  
  - **`<identifier>`** – унікальний ідентифікатор товару.  
  - **`<image>`** – URL-адреса зображення товару.  
  - **`<link>`** – URL-адреса сторінки товару на сайті.  
  - **`<old_price>`** – стара ціна товару у форматі `XXX.XX`.  
  - **`<new_price>`** – нова (акційна) ціна товару у форматі `XXX.XX`.  
  - **`<adresses>`** – список міст і магазинів, де доступний товар (структура аналогічна до `<adresses>` у `<promotion>`).  

---

### Приклад XML-документа:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<promotions>
    <promotion>
        <name>
            <uk><![CDATA[Любов у кожній знижці!]]></uk>
            <ru><![CDATA[Любов у кожній знижці!]]></ru>
        </name>
        <description>
            <uk><![CDATA[Якийсь опис]]></uk>
            <ru><![CDATA[Какое-то описание]]></ru>
        </description>
        <identifier>9925</identifier>
        <start_date>2025-02-05</start_date>
        <end_date>2025-02-18</end_date>
        <adresses>
            <item>
                <id>12</id>
                <city>
                    <name>
                        <uk>Київ</uk>
                        <ru>Киев</ru>
                    </name>
                </city>
                <shops>
                    <shop>
                        <id>12255</id>
                        <address>вул. Стрийська, 6</address>
                    </shop>
                </shops>
            </item>
        </adresses>
        <offers>
            <offer>
                <name>
                    <uk><![CDATA[Ігристе вино Maschio Prosecco Treviso Extra-dry, 11%, 0,75 л]]></uk>
                    <ru><![CDATA[Вино игристое Maschio Prosecco Treviso Extra-dry, 11%, 0,75 л]]></ru>
                </name>
                <identifier>619576</identifier>
                <image>https://image.maudau.com.ua/webp/size/lg/products/20/ed/fe/20edfe425f9376b77ec310d4e561cbca.jpg</image>
                <link>https://maudau.com.ua/product/vyno-ihryste-maschio-prosecco-treviso-extra-dry-11-075-l-619576</link>
                <old_price>499.00</old_price>
                <new_price>349.00</new_price>
                <adresses>
                    <item>
                        <id>12</id>
                        <city>
                            <name>
                                <uk>Київ</uk>
                                <ru>Киев</ru>
                            </name>
                        </city>
                        <shops>
                            <shop>
                                <id>12255</id>
                                <address>вул. Стрийська, 6</address>
                            </shop>
                        </shops>
                    </item>
                </adresses>
            </offer>
        </offers>
    </promotion>
</promotions>
```

