---
title:  "MCU Task Manager"
last_modified_at: 2025-09-24T11:00:00+03:00
categories: 
  - blog
tags:
  - learning
  - MCU
toc: true
toc_label: "Posts"
---
Коротко як просто керувати декількома завданнями через диспетчер задач

## Cтруктура коду

```с
//libs include
//function definition

void main(){
    while(1){
    
    }
}

//functions

```

*Завдання - порібно зчитати перший сенсор раз в хвилину, другий сенсор раз в 0.5 хвилини, відправити дані коли будуть готові дані із двох сенсорів, моргати світлодіодом з частотою 10Гц.*

Тобто виходить потрібно виконувати 4 завдання. Само собою це можна зробити на RTOS, але зара не про це. Уявимо що в нас слабенький проц, і має мало памяті.

## Диспетчер задач

В main пишемо менеджера завдань, flags будуть виставлятися таймером, і кожне завдання буде запускатися з потрібною частотою.

```с
if(flag[ACTION1]) Task1();
if(flag[ACTION2]) Task2();
if(flag[ACTION3]) Task3();
if(flag[ACTION4]) Task4();
HAL_Delay(1);
```

Далі нам потрібно таймер, який і буде рахувати відрізки часу та виставляти прапорці. Налаштовуємо його, щоб він викликав переривання кожної мілісекунди. Так як в нас 16-bit змінна, то можна виставти час від 1 мс до 65 535мс. Якщо потрібно рахувати більші часи то можна підкорегувати налаштування таймера або зібльшити змінну до uint32.

Кожна функція Task скидає прапорець flag\[\] та перезапускає свій таймер SetTaskTimer(). Якщо функцію потрібно запустити лише один раз, чи перестати викликати після якогось івенту, то можна просто скіпнути SetTaskTimer(). Також можна замість дефайнів TASKх_TIME можна використовувати змінну, і змінювати інтервали черезе які викликається функція Taskx().

Також можна добавити декілька функції якщо потрібно більше, просто добавити сюди ще змінні.

```с
uint8_t flag[MAX_NUM_OF_TIMERS] = {0,0,0,0};
enum {ACTION1, ACTION2, ACTION3, ACTION4};
```

## Фінальний код

```c
#define MAX_NUM_OF_TIMERS   7
#define TASK1_TIME 60000
#define TASK2_TIME 30000
#define TASK3_TIME 500
#define TASK4_TIME 100

uint8_t flag[MAX_NUM_OF_TIMERS] = {0,0,0,0};
enum {ACTION1, ACTION2, ACTION3, ACTION4};
volatile static struct
{
    uint8_t Number;
    uint16_t Time;
}SoftTimer[MAX_NUM_OF_TIMERS];

static void MX_TIM2_Init(void);

void Init(void);
void SetTaskTimer(uint8_t, uint16_t);
void Task1(void);
void Task2(void);
void Task3(void);
void Task4(void);

//timer interrupt
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
    uint8_t i;
    for(i = 0; i < MAX_NUM_OF_TIMERS; i++){
        if(SoftTimer[i].Number == 255)
            continue;     /*if timer empty, next timer*/
        if(SoftTimer[i].Time > 0){
            SoftTimer[i].Time--;
        }else{
            /*set flag*/
            flag[SoftTimer[i].Number] = 1;
            /*reset timer*/
            SoftTimer[i].Number = 255;
        }
    }
}

void main(void){
    Init();
    MX_TIM2_Init();
    
    while(1){
        if(flag[ACTION1]) Task1();
        if(flag[ACTION2]) Task2();
        if(flag[ACTION3]) Task3();
        if(flag[ACTION4]) Task4();
        HAL_Delay(1);
    }
}

static void MX_TIM2_Init(void)
{
  /* USER CODE BEGIN TIM2_Init 0 */

  /* USER CODE END TIM2_Init 0 */

  TIM_ClockConfigTypeDef sClockSourceConfig = {0};
  TIM_MasterConfigTypeDef sMasterConfig = {0};

  /* USER CODE BEGIN TIM2_Init 1 */

  /* USER CODE END TIM2_Init 1 */
  htim2.Instance = TIM2;
  htim2.Init.Prescaler = 99;
  htim2.Init.CounterMode = TIM_COUNTERMODE_UP;
  htim2.Init.Period = 484;
  htim2.Init.ClockDivision = TIM_CLOCKDIVISION_DIV1;
  htim2.Init.AutoReloadPreload = TIM_AUTORELOAD_PRELOAD_DISABLE;
  if (HAL_TIM_Base_Init(&htim2) != HAL_OK)
  {
    Error_Handler();
  }
  sClockSourceConfig.ClockSource = TIM_CLOCKSOURCE_INTERNAL;
  if (HAL_TIM_ConfigClockSource(&htim2, &sClockSourceConfig) != HAL_OK)
  {
    Error_Handler();
  }
  sMasterConfig.MasterOutputTrigger = TIM_TRGO_RESET;
  sMasterConfig.MasterSlaveMode = TIM_MASTERSLAVEMODE_DISABLE;
  if (HAL_TIMEx_MasterConfigSynchronization(&htim2, &sMasterConfig) != HAL_OK)
  {
    Error_Handler();
  }
  /* USER CODE BEGIN TIM2_Init 2 */

  /* USER CODE END TIM2_Init 2 */

}

void Init(){
    //task timer init
    uint8_t i;
    for(i = 0; i < MAX_NUM_OF_TIMERS; i++)
        SoftTimer[i].Number = 255;
    
    //timers init
    SetTaskTimer(ACTION1,TASK1_TIME);
    SetTaskTimer(ACTION2,TASK2_TIME);
    SetTaskTimer(ACTION3,TASK3_TIME);
    SetTaskTimer(ACTION4,TASK4_TIME);	
}

void SetTaskTimer(uint8_t newNumber, uint16_t newTime)
{
    uint8_t i;
    /*search existing timer*/
    for(i = 0; i < MAX_NUM_OF_TIMERS; i++){
        if(SoftTimer[i].Number == newNumber){
            /*set new time*/
            SoftTimer[i].Time = newTime;
            return;
        }
    }

    /*search new empty timer*/
    for(i = 0; i < MAX_NUM_OF_TIMERS; i++){
        if(SoftTimer[i].Number == 255){
            SoftTimer[i].Number = newNumber;
            SoftTimer[i].Time = newTime;
            return;
        }
    }
}

void Task1(void){
    flag[ACTION1] = 0;
    //do smth
    
    SetTaskTimer(ACTION1, TASK1_TIME);	
}
void Task2(void){
    flag[ACTION2] = 0;
    //do smth
    
    SetTaskTimer(ACTION2, TASK2_TIME);	
}

void Task3(void){
    flag[ACTION3] = 0;
    //do smth
    
    SetTaskTimer(ACTION3, TASK3_TIME);	
}

void Task4(void){
    flag[ACTION4] = 0;
    //do smth
    
    SetTaskTimer(ACTION4, TASK4_TIME);	
}


```

&nbsp;