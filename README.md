# Анализ данных о случаях применения силы полицией в США (2015 год)  

---

## Основная часть  

### 1. Набор данных  
Датасет включает данные об убийствах полицией в США в 2015 году.  
Характеристики:  
- Формат: CSV  
- Количество признаков: 34  
- Количество записей: 468  

Примеры атрибутов:  
- name — имя умершего  
- age — возраст  
- gender — пол  
- raceethnicity — этническая принадлежность  
- month, day, year — дата происшествия  
- city, state — место происшествия  
- cause — причина смерти  
- armed — был ли вооружен  
- income, urate, college — социальные показатели района  

---

### 2. Архитектура конвейера для предобработки данных  
Для анализа использовались следующие инструменты:  

- MariaDB — база данных для хранения  
- Apache Hive — SQL-интерфейс для работы с данными в HDFS  
- Apache Sqoop — передача данных между реляционными БД и Hadoop  
- Apache Kafka — потоковая обработка  
- Apache Flume — управление потоками данных  

Этапы конвейера:  
1. Запуск служб HDFS и YARN
   
   <img width="1004" height="424" alt="image" src="https://github.com/user-attachments/assets/d9bcf32e-72b8-44bd-b0d6-21c3496ed131" />

3. Создание таблицы police_killings в MariaDB
   
   <img width="378" height="553" alt="image" src="https://github.com/user-attachments/assets/d93945ca-c127-43c7-b0a3-e08a91639956" />

5. Экспорт данных в MariaDB (через Sqoop)
   
   <img width="974" height="352" alt="image" src="https://github.com/user-attachments/assets/1d52497a-318a-4b70-96be-b8f459fafc19" />

7. Очистка и приведение типов данных
   
   <img width="641" height="367" alt="image" src="https://github.com/user-attachments/assets/c82ce0f4-c3c8-458e-b111-c3212a6a8543" />
 <img width="636" height="436" alt="image" src="https://github.com/user-attachments/assets/fee23320-a1ce-471c-8e3a-54d7b21cbd19" />

9. Перенос данных в Hive
    
    <img width="758" height="549" alt="image" src="https://github.com/user-attachments/assets/2619e7a5-707a-49ce-b14f-08736a50849f" />

11. Настройка потоковой передачи (Kafka + Flume)
    
    <img width="687" height="606" alt="image" src="https://github.com/user-attachments/assets/cab1b448-136e-4c09-9e71-66152de923b1" />
    <img width="588" height="513" alt="image" src="https://github.com/user-attachments/assets/fdffe380-463f-4f7a-a5a5-4059171ded91" />
<img width="774" height="849" alt="image" src="https://github.com/user-attachments/assets/68f858a7-85d8-449b-9026-e86d7bcc9f40" />

13. Организация регулярной выборки и записи данных в HDFS  

---

## Анализ данных  

### 2.1 География убийств  

<img width="974" height="500" alt="image" src="https://github.com/user-attachments/assets/1a0908ca-96e3-49aa-a857-41b8511f06ae" />

<img width="804" height="432" alt="image" src="https://github.com/user-attachments/assets/1323224d-0a91-45d7-bda9-a232a4b6849e" />

<img width="961" height="913" alt="image" src="https://github.com/user-attachments/assets/8ceafda9-6ab1-46a1-a06c-dbe9a0cc55fb" />

- Наибольшее количество смертей: Калифорния, Техас, Флорида  
- Также высокий уровень: Аризона, Оклахома  
- Корреляция с населением, но важны и криминогенные факторы.  

### 2.2 Динамика по времени  

<img width="974" height="260" alt="image" src="https://github.com/user-attachments/assets/30bf4dad-ecb9-4e36-ab7f-6126cbb67d6b" />

<img width="974" height="516" alt="image" src="https://github.com/user-attachments/assets/f2be4eb5-5dd7-41f6-8d5a-267da8b3332c" />

<img width="974" height="521" alt="image" src="https://github.com/user-attachments/assets/4275e15b-6982-41d0-a00f-8469ca688294" />

- Пик смертей: март–апрель  
- Минимум: июнь  
- Выражена сезонность.  

### 2.3 Возраст  

<img width="974" height="516" alt="image" src="https://github.com/user-attachments/assets/ca294230-628e-4b99-b18c-fffdfcb496e5" />

<img width="974" height="636" alt="image" src="https://github.com/user-attachments/assets/10a8f445-4fa2-4646-a8b5-9392d2335601" />

<img width="974" height="486" alt="image" src="https://github.com/user-attachments/assets/bc8d471b-3614-43b3-837e-7b5ec12bc50a" />

- Чаще всего жертвы: мужчины 25–37 лет  
- Женщины — в возрасте 30+  
- У мужчин разброс шире.  

### 2.4 Предпочтение оружия  

<img width="990" height="360" alt="image" src="https://github.com/user-attachments/assets/8e1703fa-6907-479c-9b9f-2d71e20b5fb5" />

<img width="695" height="472" alt="image" src="https://github.com/user-attachments/assets/96fc9de9-dd6a-4aac-9fec-a072c5260383" />

<img width="649" height="606" alt="image" src="https://github.com/user-attachments/assets/5350b61a-1142-4e4c-afbd-bd43570756e9" />

- Наиболее частая причина: огнестрельное оружие  
- У мужчин на 3 месте — ножи  
- У женщин на 3 месте — транспортные средства.  

### 2.5 Доход  

<img width="974" height="556" alt="image" src="https://github.com/user-attachments/assets/2684aa98-79b2-46dd-b4ee-7a2dde342bf9" />


- Средний доход жертв: ниже среднего по США  
- Мужчины — $18–29 тыс.  
- Женщины — $21–34 тыс.  

### 2.6 Этническая принадлежность  

<img width="974" height="479" alt="image" src="https://github.com/user-attachments/assets/df55bf87-0243-46af-9e93-37c9ca1e2524" />

<img width="974" height="473" alt="image" src="https://github.com/user-attachments/assets/5e659357-b3ae-45f8-bcdc-4199d320f74a" />


- Белые — 202 человек  
- Темнокожие — 118 человек  
- Латиноамериканцы — 59  
- Азиаты — 9  

По соотношению к населению:  
- Темнокожие: 0.19  
- Белые: 0.09  
- Латиноамериканцы: 0.06  
- Азиаты: 0.04  

---

## Выводы  

- Жертвами чаще становятся молодые мужчины (25–37 лет).  
- Самая уязвимая группа — темнокожие мужчины с низким доходом.  
- Наибольшая частота смертей наблюдается в крупных и криминогенных штатах.  
- Чаще всего причиной служит огнестрельное оружие.    
