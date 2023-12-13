## ER ##

@startuml
entity "Клиент" as cl {
cl_code <<generated>>
--
First_name
Last_name
Middle_name
Birthday
City
Country
Phone_number
}

entity "Отделение" as br {
Branch_code <<generated>>
--
adress
City
Country
}

entity "Сотрудник" as emp {
emp_code <<generated>>
--
First_name
Last_name
Middle_name
City
Country
Short_Phone_number
Branch_code <<FK>>
Head_Ofice
Position
}

entity "Заказ" as od {
Order_code <<generated>>
--
cl_code <<FK>>
принят сотрудником (emp_code <<FK>>)
service_code <<FK>>
City
Date_of_order
Date_release
Channel_of_sale_code <<FK>>
}

entity "Тип услуги" as ser {
service_code <<generated>>
--
Name of service
Ctype_code <<FK>>
}

entity "Канал продаж" as channel {
channel_code <<generated>>
--
Name of channel: Отделение, МП, внешние
}


entity "Тип карты" as C_type {
Ctype_code <<generated>>
--
C_type_name
}

entity "Выданные карты" as cards {
Card_number 
Account
--
cl_code <<FK>>
Выдана в отделении: Branch_code <<FK>>
Выдана сотрудником: emp_code <<FK>>
Ctype_code <<FK>>
order_code <<FK>>
City
Limit
Currency_code <<FK>>
Date of activation
Date of expire
}

entity "Валюта" as cur {
Cur_code <<generated>>
--
Currency_name
Currency_CB_code
}


cl ----{ od
emp ----{ od
ser ----{ od
ser ----o| C_type
cur ----{ cards
cl ----{ cards
emp }----o| br
br |o----{ cards
od ----o{ cards
C_type ----{ cards
channel ----{ od
cards}---- emp
@enduml
