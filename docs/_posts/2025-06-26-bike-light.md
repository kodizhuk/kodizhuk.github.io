---
title:  "Вело світло"
last_modified_at: 2025-06-26T17:04:08-04:00
categories: 
  - blog
tags:
  - teardowns
toc: true
toc_label: "Posts"
---

Розбірка, схема, і переробка на Type-C зарядку для вело ліхтаря Oneride

![bike-light-1.png](/assets/resources/bike-light-1.png)

## Характеристики
**Параметри **(із сайту виробника**)**:

- Виробник: Oneride
- Ємність акумулятора: 500 mAh
- Світловий потік: 65 Лм
- Зарядне: Micro USB
- Час зарядки: 2 години

**Режими роботи:**

- Постійний нормальний (25%) - до 6.5 годин
- Постійний середній (50%) - до 3 годин
- Постійний яскравий (100%) - до 1.75 години
- Повільно блимаючий нормальний (25%) - до 5.5 годин
- Повільно блимаючий яскравий (100%) - до 3 годин
- Швидко блимаючий середній (50%) - до 4 годин

**Виміряні дані:**

| Режим | Струм споживання |
| --- | --- |
| Мінімальна яскравість | 100 mA |
| Середня яскравість | 200 mA |
| Максимальна яскравість | 400 mA |
| Виключений (2.7V акум) | 0.12 mA |
| Виключений (4.2V акум) | 0.2 mA |

Тобто на макс яскравості виходить що ліхтарик зможе просвітити в кращому випадку 500mAh/400mA = 1.25год, а сказали що світитиме 1.75год, трохи надбавили.

Струм споживання постійний і не змінюється при розрядці акумулятора, це означає що є LED драйвер, і ліхтарик світитиме однаково коли акум заряджений і коли розряджений.

Ліхтарик автоматично вимкнеться при розряді акумулятора до 2.4V. Щоб девайс знову запустився потрібно щоб напруга на акумуляторі була більшою за 2.7V.

## Схема

![bike-light-2.png](/assets/resources/bike-light-2.png)

Список компонентів:

- MEL7136A - Linear Adjustable Constant Current LED Driver
- MCU - затерта назва, 4 ніжки
- XT4054 - мікросхема зарядки акумулятора, до 500mA макс.
- D33Y - якась LDO, можливо AP7370-33Y-13

![bike-light-3.png](/assets/resources/bike-light-3.png)

![bike-light-4.png](/assets/resources/bike-light-4.png)

![bike-light-5.png](/assets/resources/bike-light-5.png)

## Заміна Micro USB на USB Type-C

При використанні роз'єму Type-C просто перепаяти коннектор замість micro USB не вийде. В micro USB напруга завжди 5V. Яку зарядку не підключиш - завжди буде живлення 5V. Type-C ж може видавати різну напругу (за умови використання Type-C to Type-C шнура. Якщо кабель Type-A to Type-C то буде лише 5V).

У Type-C виводів багато (якщо якісь не використовуються, то їх часто просто не підключають)

![bike-light-6.png](/assets/resources/bike-light-6.png)

Нам потрібно сказати зарядному пристрою щоб він нам видав 5V. Для цього на виводи CC потрібно повісити резистор 5.1kOhm. В цьому випадку зарядний пристрій максимум зможе видати на пристрій до 15W при напрузі 5V. 

На алі продаються ось такі роз'єми USB Type-C, там де стрілка треба запаяти резистор, і тоді цей роз'єм працюватиме з будь-яким зарядним пристроєм.


![bike-light-7.png](/assets/resources/bike-light-7.png)

![bike-light-8.png](/assets/resources/bike-light-8.png)

![bike-light-9.png](/assets/resources/bike-light-9.png)
![bike-light-10.jpg](/assets/resources/bike-light-10.jpg)
![bike-light-11.jpg](/assets/resources/bike-light-11.jpg)
![bike-light-12.jpg](/assets/resources/bike-light-12.jpg)
![bike-light-13.jpg](/assets/resources/bike-light-13.jpg)
![bike-light-14.jpg](/assets/resources/bike-light-14.jpg)
![bike-light-15.jpg](/assets/resources/bike-light-15.jpg)
![bike-light-16.jpg](/assets/resources/bike-light-16.jpg)
![bike-light-17.jpg](/assets/resources/bike-light-17.jpg)
![bike-light-18.jpg](/assets/resources/bike-light-18.jpg)
![bike-light-19.jpg](/assets/resources/bike-light-19.jpg)