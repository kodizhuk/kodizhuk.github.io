---
title:  "Повербанк для дому"
last_modified_at: 2024-10-30T11:00:00+03:00
categories: 
  - blog
tags:
  - projects
toc: true
toc_label: "Posts"
---

Повербанк для квартири на LiFePO4 акумуляторах.

![home-powerbank-1.png](/assets/resources/home-powerbank-1.png)


## Технічне завдання

Через російську агресію та атаку на Українську інфраструктуру час від часу відбувається вимкнення світла. Графік увімкнення світла у Львові можуть міняти по декілька разів на день.

<figure>
  <a href="/assets/resources/home-powerbank-2.png"><img src="/assets/resources/home-powerbank-2.png" style="width: 25vw; min-width: 15px;"></a>
</figure>

Тому нарешті дійшли руки щоб замовити акумулятори та зібрати повербанк для квартири. Ми живемо на орендованій квартирі, тому ТЗ трішки специфічне.

- потужність 3кВт макс мало би хватити на квартиру
- основні пристрої які повинні працювати: котел газовий, холодильник, світло
- ємність акумулятора десь 6кВт\*год мало би хватити
- окремо стояча на коліщатах, щоб при можливості можна було просто перенести на іншу квартиру

## Компоненти

1.  Інвертор на 3кВт
2.  акумулятор LiFePO4 на 280Ah, 8 шт
3.  плата BMS на 200А
4.  корпус

## Інвертор

PowMr 3000W Hybrid Solar Inverter, купував на [алі](https://www.aliexpress.com/item/1005004819832099.html?spm=a2g0o.order_list.order_list_main.162.eec21802GAbQNP#nav-specification)

Основні параметри:

| модель| POW-HVM3.2H-24V-N|
| напруга| 24В|
| потужність| 3кВт|
| макс струм для зарядки акумуляторів від мережі| 60А (1440Вт)|
| підключення | WiFi | |
| моніторинг | потужність <br> наявність менержі <br> заряд акумулятора
    
<figure>
  <a href="/assets/resources/home-powerbank-3.png"><img src="/assets/resources/home-powerbank-3.png" style="width: 15vw; min-width: 15px;"></a>
</figure>    

## Акумулятори

Акумулятори я брав LiFePO4. Замовляв на сайті [deligreencs.com](https://deligreencs.com/products/lifepo4-battery-eve-280ahk-8000-cycles-grade-a)

| ємність | 280 Ah (896 Wh) |
| номінальна напруга | 3.2 V |
| робоча напруга | 2.5V-3.65V |
| макс струм заряду | 1С (тобто 280А) |
| рекомендований струм розряду | 0,5С (140А) <| > макс 3С ( тобто 840А) |
| кількість циклів заряду | 8000 (до 80% ємності) |
| маса одного | 5,5 Кг |
| Кріплення шин болти | М6 |


Ішли більше 2 місяців, прийшли гарно запаковані, опір тож ніби ок.

<figure>
  <a href="/assets/resources/home-powerbank-4.png"><img src="/assets/resources/home-powerbank-4.png" style="width: 15vw; min-width: 15px;"></a>
  <a href="/assets/resources/home-powerbank-5.png"><img src="/assets/resources/home-powerbank-5.png" style="width: 15vw; min-width: 15px;"></a>
  <a href="/assets/resources/home-powerbank-6.png"><img src="/assets/resources/home-powerbank-6.png" style="width: 15vw; min-width: 15px;"></a>
</figure>


## Плата BMS

Купив від Jikong. Робочий струм розраховується в залежності від потужності інвертора. В мене на 3000 Вт / 24 В = 125А. Я взяв із запасом на 200 А.

| модель | JK-B1A8S20P |
| напргуга | 3-8S (9.6V - 25.6V) |
| струм | 200A (піковий 350А) |
| струм балансування | 1А |
| інтерфейс | блютуз |

<figure>
  <a href="/assets/resources/home-powerbank-7.png"><img src="/assets/resources/home-powerbank-7.png" style="width: 15vw; min-width: 15px;"></a>
</figure>

Апку на андроїд можна скачати з [PlayMarket](https://play.google.com/store/apps/details?id=com.jktech.bms)

<figure>
  <a href="/assets/resources/home-powerbank-9.png"><img src="/assets/resources/home-powerbank-9.png" style="width: 15vw; min-width: 15px;"></a>
</figure>

## Корпус

Я спочатку хотів купити готовий металевий. Продається на алі, або можна найти на [prom.ua](http://prom.ua/). Але його вартість трішки кусається, десь в районі 8к грн на 8 акумуляторів. Тому вирішив замовити порізку з дсп, типу тумбочка.

Намалював модель в oneshape, замовив у Львові, десь за тиждень зробили. Модель та всі креслення доступні для редагування ось тут [OneShape](https://cad.onshape.com/documents/a14eecb62d29b860f6b12bec/w/0b682ec30c09bee4485dcb84/e/76a46c6da80f7123c9651ecc?renderMode=0&uiState=6707d0970a76693ecd81cf8b)

<figure>
  <a href="/assets/resources/home-powerbank-10.png"><img src="/assets/resources/home-powerbank-10.png" style="width: 15vw; min-width: 15px;"></a>
</figure>

## Підключення

Газовий котел потребує заземлення. Якщо котел до інвертора напряму, то котел покаже помилку і не запуститься. Десь почитав на просторах інтернету що котел є фазозалежним, тобто котлу потрібна чітка фаза на одному дроті а нуль на іншому. А якщо тикнути тестером напруги (така викрутка з лампочкою) на кожен вихід з інвертора, то він буде світитися на двох виходах, тобто виходить ніби дві фази. Тому одну з низ треба зробити нулем.

Якщо автоматом відключити фазу та нуль від міста, тоді нуля в квартирі не буде, і котел працювати без нуля тож не буде.

<figure>
  <a href="/assets/resources/home-powerbank-11.png"><img src="/assets/resources/home-powerbank-11.png" style="width: 30vw; min-width: 15px;"></a>
</figure>

В моєму варіанті підключення, і вхідний автомат не вимикаю, і виходить інвертор бере нуль від міста через дріт який позначений “зарадка акумулятора”.

Але це все на ваш страх та ризик! Якщо щось спалите то буде самі винуваті.

У мене підключення до квартири виглядає ось так

<figure>
  <a href="/assets/resources/home-powerbank-12.png"><img src="/assets/resources/home-powerbank-12.png" style="width: 30vw; min-width: 15px;"></a>
</figure>

## Загальна вартість

| інвертор | 230$ |
| акумулятори 8шт | 682$ |
| плата BMS | 68$ |
| корпус | 36$ |
|  | 1016$ |

Вийшла така собі невеликий повербанк для квартири на 896Wh\*8 = 7168Wh ємності.

**Плюси**:
- при розрахунку що квартира буде споживати десь нехай 300W в середньому, то мало би хватити майже на 24 години безперервної роботи.
- Дуже зручно з коліщатками, можна відкотити в іншу частину квартири щоб не заважала коли не використовується.
- зарядка акумів іде струмом 60А, тобто десь виходить потрібно 4.6 год щоб повністю зарядити. Як на мене досить непогано, враховуючи з поточними відключеннями він розряджається лише до 80%.

**Недоліки** :
- інвертор голосно шумить при потужності більшій за 400 W. При зарядці в тому числі. В квартирі трішки напрягає. Треба доробити регулювання швидкості по температурі радіаторів.
- коли підключений навіть без навантаження, то час від часу вмикає вентилятори