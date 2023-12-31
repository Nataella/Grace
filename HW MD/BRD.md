![alfa](https://github.com/Nataella/Grace/assets/151657470/14336400-42c9-4cf9-b231-7570decb876d)



#  Бизнес функциональные требования:  <br>  "Доставка карты курьером". #

**История изменений**


|Дата|Описание изменений|версия|Автор|Бизнес-заказчик|Согласование бизнес-заказчика|
|----|-------------------|--------|-----------|------------------|-----------------------------------|
|17.12.2023|Разработка функционала доставка карты курьером|1.0|Савина Н.|Иванов И.|согласовано

1. **Оглавление**
 
*	*Общая информация	4*  
*	*Бизнес цели и бизнес требования	4*  
*  	*Функциональные требования	4*  
*	*Нефункциональные требования*  
*	*Возможность поэтапного внедрения*  
*	*Критерии приёмки функционала	4*  
*	*Приложения	4*  

**Общая информация**
1. Термины и определения
  
|Термин|Определение|
|----|-------------------------------------------------------------------------------------------|
|Клиент|Авторизированный действующий клиент банка|
|ОВК|Отдел выпуска карт|
|Курьер|Сотрудник курьерской службы, осуществляющий доставку карты|
|Бэкофис|Сотрудник бэкофис, сопровождающий выдачу карты|
|Сайт|Личный кабинет авторизированного клиента|
|ЮД|Юридический департамент|
|МП|Мобильное приложение|

2. Ссылки на существующую документацию

|Описание|Ссылка|
|----|-------------------------------------------------------------------------------------------|
|  - |  -  |

3. Контактные лица

|Подразделение|Роль в процессе |ФИО|
|----|-------------------|-------------------|
|Бизнес|Product owner|Иванов И|
|ИТ|Системный аналитик|Савина Н|

* **Бизнес цели и бизнес требования**

&nbsp;&nbsp;&nbsp;&nbsp; Цель данной доработки заключается в увеличении объемов продаж банка через обеспечение удобных условий предоставления услуг клиентам и как следствие увеличение прибыли банках. 

&nbsp;&nbsp;&nbsp;&nbsp; В данный момент банк не предлагает услугу доставки карт курьерами. Для осуществления этой задачи необходимо закдлючить договор с курьерсокой службой N, разработать софт, позволяющий курьерам предоставлять услуги банка удалено. Так же необходимо разработать юридическое обоснование этой возможности.

* **Функциональные требования**

1.	В системе/интерфейсе/личном кабинете доступен функционал заказа банковской карты. В данный момент клиент может заказать эту карту через МП с получением в отделении. Нужно добавить окошко выбора доставки карты курьером.
- Когда клиент ставит галку в этом окошке, значит, он хочет получить карту через курьера.
- После этого клиенту зстановится доступными поля ввода адрес. Введенный клиентом адрес должен сверяться на соответствие зоне доставки.
- После введения адреса, клиенту открываются поля с доступными датами и временем, когда он готов встретиться с курьером.
- После выбора клиентом даты и времени, клиент получает уведомление "заявка на проверке", а заявка поступает в бэкофис на проверку.
- По результатам проверки заявка либо отклоняется и клиент получает увеломление "заявка отклонена", либо заявка передается в ОВК.

2.	Курьер должен иметь право доступа к системе банка через мобильное устройство, чтобы подгружать в личную карточку клиента его подпись и фото с картой.

*	**Нефункциональные требования**

1. Окошко для галочки должно быть светлого, но не белого цвета, квадратным.
2. Окошко должно располагаться над кнопкой «заказать».
3. Приложение для курьеров должно быть разработано для мобильных устройств с ОС IOS, Android. 
4. Приложение должно работать в полной мере от мобильного интернета. 
5. Загрузка документов не должна длиться более минуты.

*	**Возможность поэтапного внедрения**

  Обе части доработки должны проходить параллельно друг другу. 

*	**Критерии приёмки функционала**

Разработка отчета тестирования. Отчет должен содержать не менее 100 итераций, имитирующих выдачу курьером карты клиенту. По каждой итерации фиксируется результат: успешный, если удалось получить статус "карта выдана", и неуспешный - в остальных случаях. Допустимым результатом для принятия функционала является доля неуспешных статусов менее 3% (Приложение 1). 


*	**Приложения**
	
Приложение 1. Отчет о реализации задачи.

|Номер итерации|результат|
|----|-------------------------------------------------------------------------------------------|
|  1 |  ...  |
|  ... |  ...  |
|  n |  ...  |

Приложение 2. Схема процесса.

<https://drive.google.com/file/d/1LitJiJ0MwQyOzeVKaC2xykPyvkSG3vfz/view?usp=sharing>

![Диаграмма без названия](https://github.com/Nataella/Grace/assets/151657470/a7bee480-4944-4d7d-a971-a854de916b29)



