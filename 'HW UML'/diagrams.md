Use Case
  
  @startuml
left to right direction
actor "Клиент" as cl
package "Банк" {
actor "Сайт" as site
actor "Бэкофис" as BO
actor "Отдел выпуска карт" as CI
}
actor "Курьер" as car
rectangle "Доставка карты курьером" {
usecase "выбрать доставку карты курьером" as UC1
usecase "заполнить поля: адрес, дата и время доставки" as UC2
usecase "проверить введенный адрес на соответсвие зоне доставки" as UC3
usecase "менять статус заявки" as UC4
usecase "проверить заявку" as UC5
usecase "выпустить карту" as UC6
usecase "доставить карту" as UC7
usecase "идентифицировать клиента" as UC8
usecase "выдать карту" as UC9
usecase "соответствует зоне доставки" as UC10
usecase "не соответствует зоне доставки" as UC11
usecase "получить карту" as UC12
usecase "Получить подпись" as UC13
usecase "Загрузить фото клиента с картой" as UC14
}
cl --> UC1
UC3 <-- UC10
UC3 <-- UC11
UC1 <. UC2: <<include>>
cl --> UC12
site --> UC3
site --> UC4
BO --> UC5
CI --> UC6

car --> UC7
car --> UC8
car --> UC9
UC8 <. UC13: <<include>>
UC8 <. UC14: <<include>>
@enduml

  Sequence

  @startuml
mainframe **sd** "Заказ кредитной карты в приложении"
actor "Клиент" as cl
participant "МП" as app
participant Eq  as Eq 
'Eq Система, в которой хранятся данные клиента
participant "Кредитный конвейер КК" as CC
participant "Скоринг" as Sc
participant "Продуктовый Каталог" as PC
participant "Справочник Отделений Банка" as sob
database "База данных Банка" as BDB
database "Внешняя База данных" as EBD
actor "Отдел выпуска КК" as CD

activate cl
activate app
loop 3 раза
 alt авторизация клиента
  cl -> app:  авторизация по faci_id
 else
  cl -> app:  авторизация по логину и паролю
 end
  app -> Eq: сравнение введенных данных с регистрационными данными в БД 
activate Eq   
    Eq --> app: данные совпадают

group neg
    Eq --> app: данные не совпадают
deactivate Eq 
    app -> cl: возврат к экрану входа   
 end 

end

app --> cl: авторизация в системе
cl -> app: переход на страницу выбора продукта
app -> PC: запрос доступных продуктов
activate PC
PC --> app: загрузка достпных продуктов
deactivate PC
app --> cl: отображение доступных продуктов
cl -> cl: заполнение данных по продукту (выбор продукта КК)
cl -> app: ввод данных
app -> cl: как удобно получить карту (в отделении\ курьером)
 alt
  cl --> app: курьер
  else 
  cl --> app: получу в отделении
  app-> Eq: поиск города в регистрационных данных клиента
activate Eq
  Eq--> app: результат поиска города
deactivate Eq
  app-> cl: ваш город Такой-то?
   alt
    cl --> app: да
    app-> sob: запрос на список отделений в городе Таком-то
activate sob
    sob --> app: возврат списка отделений
deactivate sob
   else 
    cl --> app: нет
    app-> cl: Введите ваш город
    cl -> app: Город Другой
    app-> sob: запрос на список отделений в городе Другом
activate sob
    sob --> app: возврат списка отделений
deactivate sob 
   end
    app-> cl: выберете удобное вам отделение
    cl -> app: выбор отделения
 end
app-> cl: заполните анкету на получение КК

cl ->> app: заполнение формы заявки
deactivate cl

app -> CC: передача заявки клиента в кредитный конвейер
deactivate app
activate CC

 Alt Получение предложения для клиента
   Alt Проверка Клиента
    
    CC -> BDB: проверка клиента по внутренним базам банка
activate BDB
    BDB--> CC: проверку прошел
deactivate BDB
    CC -> EBD: проверка клиента по внешним базам банка
activate EBD
    EBD--> CC: проверку прошел
deactivate EBD
   else  проверку не прошел
  CC --> app: проверку не прошел
activate app
    app --> cl: отказ
deactivate app
   end
 CC-> Sc: расчет кредитного предложения
activate Sc
 Sc-> CC: клиенту одобрена КК под рассчитанные условия
 deactivate Sc
 else отказ
 CC --> app: не смогли сделать предложение клиенту
activate app
 app --> cl: отказ
deactivate app
 end

par
CC --> app: заявка одобрена
activate app
CC -> CD: передача успешной заявки в отдел выпуска карт
end
deactivate CC
app-> cl: заявка одобрена.
deactivate app
@enduml
