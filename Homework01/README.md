Homework 01

На схеме изображена модель БД для интернет магазина, 

Задачи которая решает БД
1. Поставщики могут узнать какие товары производят производители и связаться с ними
2. Покупали могу узнать какие товары продают продавцы и связаться с ними
3. Фиксируются покупки товаров покупателями
4. возможна аналитика покупок (какие товары покупают покупатели и у каких поставщиков)
5. возможен обзвон клиентов

# Описание таблиц и полей

## Таблица Addresses 
Таблица содержит адреса (производителей и покупателей)
1. address id - главный ключ таблицы, integer
2. country - страна, varchar
3. city - город, varchar
4. street - улица, varchar
5. building - номер дома, varchar
6. appartaments - номер квартиры, integer

## Таблица Prices
Таблица содержит цены на товары
1. price id - главный ключ таблицы, integer
2. price - цена

## Таблица Customers
Таблица содержит информацию о покупателях
1. customer id - главный ключ таблицы, integer
2. name - имя покупателя
3. surname - фамилия покупателя
4. address id - внешний ключ, адрес покупателя, integer
5. phone id - внешний ключ, телефон покупателя, integer

## Таблица Dealers
Таблица содержит инйормацию о продавцах и товарах которые они продают
1. dealer id - главный ключ таблицы, integer
2. dealer - имя продавца, varchar
3. phone id - внешний ключ, телефон продавца, integer
4. product id - внешний ключ, id продаваемого товара, integer

## Таблица Purchases
Таблица содержит информацию  о покупках  ( какой покупатель у какого продавца какой товар когда купил)
1. purchase id - главный ключ таблицы, integer
2. product id - внешний ключ, id продаваемого товара, integer
3. dealer id - внешний ключ, id продавца, integer
4. price id - внешний ключ, id цены, integer
5. customer id - внешний ключ, id покупателя, integer
6. date - врема покупки товара, date/time

## Таблица Phones
Таблица собержит номера телефоном ( покупателей продавцов и производителей )
1. phone id - главный ключ таблицы, integer
2. number - номер телефона, varchar
3. operator - сотовый оператор, varchar

## Таблица Manufactures
Таблица содержит данные о производителях и производимых товарах
1. manufacture id - главный ключ таблицы, integer
2. manufacture - имя производителя, varchar
3. address id - внешний ключ, адрес производителя, integer
4. phone id - внешний ключ, телефон производителя, integer
5. product id - внешний ключ, id производимого товара, integer

## Таблица Products
Таблица содержит информацию о товаре
1. product id - главный ключ таблицы, integer
2. name - наименование товара, varchar
3. category id - внешний ключ, категория товара, integer
4. description - описание товара, varchar

## Таблица Product categories
1. category id - - главный ключ таблицы, integer
2. name - наименование  категории, varchar










