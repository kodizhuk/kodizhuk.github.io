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

Розбірка, схема і переробка на Type-C зарядку для вело ліхтаря Oneride

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

Струм споживання постійний і не змінюється при розрядці акумулятора, це означає що є LED драйвер, і ліхтарик світитиме однаково коли акум заряджений та коли розряджений.

Ліхтарик автоматично вимкнеться при розряді акумулятора до 2.4V. Щоб девайс знову запустився потрібно щоб напруга на акумуляторі була більшою за 2.7V.

## Схема

<figure>
  <a href="/assets/resources/bike-light-2.png">
    <img src="/assets/resources/bike-light-2.png" alt="diagram">
  </a>
</figure>

Список компонентів:

- MEL7136A - Linear Adjustable Constant Current LED Driver
- MCU - затерта назва, 8 ніжок
- XT4054 - мікросхема зарядки акумулятора, до 500mA макс
- D33Y - якась LDO, можливо AP7370-33Y-13

<figure class="two">
  <img src="/assets/resources/bike-light-3.png" style="width: 12vw; min-width: 15px;">
  <img src="/assets/resources/bike-light-4.png" style="width: 15vw; min-width: 15px;">
</figure>
<figure>
  <a href="/assets/resources/bike-light-5.png"><img src="/assets/resources/bike-light-5.png" alt="components"></a>
</figure>

## Заміна Micro USB на USB Type-C

При використанні роз'єму Type-C просто перепаяти коннектор замість micro USB не вийде. В micro USB напруга завжди 5V. Яку зарядку не підключиш - завжди буде живлення 5V. 
Type-C ж може видавати різну напругу (за умови використання Type-C<==>Type-C шнура. Якщо кабель Type-A<==>Type-C то буде лише 5V).

У Type-C виводів багато (якщо якісь не використовуються, то їх часто просто не підключають)

![bike-light-6.png](/assets/resources/bike-light-6.png)

Нам потрібно сказати зарядному пристрою щоб він нам видав 5V. Для цього на виводи CC потрібно повісити резистор 5.1kOhm. В цьому випадку зарядний пристрій максимум зможе видати на пристрій до 15W при напрузі 5V. 

На алі продаються ось такі роз'єми USB Type-C, там де стрілка треба запаяти резистор, і тоді цей роз'єм працюватиме з будь-яким зарядним пристроєм.

![bike-light-7.png](/assets/resources/bike-light-7.png)

![bike-light-8.png](/assets/resources/bike-light-8.png)

![bike-light-9.png](/assets/resources/bike-light-9.png)

## Фото

<a href="/assets/resources/bike-light-10.jpg"><img src="/assets/resources/bike-light-10.jpg" style="width: 5vw; min-width: 10px;" ></a>
<a href="/assets/resources/bike-light-11.jpg"><img src="/assets/resources/bike-light-11.jpg" style="width: 5vw; min-width: 10px;" ></a>
<a href="/assets/resources/bike-light-12.jpg"><img src="/assets/resources/bike-light-12.jpg" style="width: 6vw; min-width: 10px;" ></a>  
<a href="/assets/resources/bike-light-14.jpg"><img src="/assets/resources/bike-light-14.jpg" style="width: 5vw; min-width: 10px;"></a>
<a href="/assets/resources/bike-light-13.jpg"><img src="/assets/resources/bike-light-13.jpg" style="width: 5vw; min-width: 10px;"></a>
<a href="/assets/resources/bike-light-15.jpg"><img src="/assets/resources/bike-light-15.jpg" style="width: 5vw; min-width: 10px;"></a>
<a href="/assets/resources/bike-light-16.jpg"><img src="/assets/resources/bike-light-16.jpg" style="width: 5vw; min-width: 10px;"></a>
<a href="/assets/resources/bike-light-17.jpg"><img src="/assets/resources/bike-light-17.jpg" style="width: 5vw; min-width: 10px;"></a>
<a href="/assets/resources/bike-light-18.jpg"><img src="/assets/resources/bike-light-18.jpg" style="width: 5vw; min-width: 10px;"></a>
<a href="/assets/resources/bike-light-19.jpg"><img src="/assets/resources/bike-light-19.jpg" style="width: 5vw; min-width: 10px;"></a>