Homework 02

# Обновленное описание таблиц и полей

### Таблица Addresses 
Таблица содержит адреса (производителей и покупателей)
1. address id - главный ключ таблицы. integer,PRIMARY KEY
2. address owner id - ключ, по которому у одного покупателя или производителя может быть несколько адресов, integer, NOT NULL
3. country - страна, varchar
4. city - город, varchar
5. street - улица, varchar
6. building - номер дома, varchar
7. appartaments - номер квартиры, varchar

### Таблица Prices
Таблица содержит цены на товары
1. price id - главный ключ таблицы, integer, PRIMARY KEY
2. price - цена, NOT NULL, UNIQUE

### Таблица Customers
Таблица содержит информацию о покупателях
1. customer id - главный ключ таблицы, integer, PRIMARY KEY
2. name - имя покупателя, varchar, NOT NULL
3. surname - фамилия покупателя
4. address owner id - внешний ключ, адрес покупателя, integer, FOREIGN KEY
5. phone owner id - внешний ключ, телефон покупателя, integer, FOREIGN KEY

### Таблица Dealers
Таблица содержит инйормацию о продавцах и товарах которые они продают
1. dealer id - главный ключ таблицы, integer, PRIMARY KEY
2. dealer - имя продавца, varchar, NOT NULL
3. phone owner id  - внешний ключ, телефон продавца, integer, FOREIGN KEY
4. product id - внешний ключ, id продаваемого товара, integer, FOREIGN KEY

### Таблица Purchases
Таблица содержит информацию  о покупках  ( какой покупатель у какого продавца какой товар когда купил)
1. purchase id - главный ключ таблицы, integer, PRIMARY KEY
2. product id - внешний ключ, id продаваемого товара, integer, FOREIGN KEY
3. dealer id - внешний ключ, id продавца, integer, FOREIGN KEY
4. price id - внешний ключ, id цены, integer, FOREIGN KEY
5. customer id - внешний ключ, id покупателя, integer, FOREIGN KEY
6. date - врема покупки товара, date/time, NOT NULL DEFAULT CURRENT_DATE

### Таблица Phones
Таблица собержит номера телефоном ( покупателей продавцов и производителей )
1. phone id - главный ключ таблицы, integer, PRIMARY KEY
2. number - номер телефона, varchar, NOT NULL, UNIQUE
3. operator - сотовый оператор, varchar
4. phone owner id  - ключ, по которому у одного покупателя или производителя может быть несколько телефонов, integer,  NOT NULL

### Таблица Manufactures
Таблица содержит данные о производителях и производимых товарах
1. manufacture id - главный ключ таблицы, integer, PRIMARY KEY
2. manufacture - имя производителя, varchar, NOT NULL, UNIQUE
3. address id - внешний ключ, адрес производителя, integer, FOREIGN KEY
4. phone id - внешний ключ, телефон производителя, integer, FOREIGN KEY
5. manufactured item id - ключ, по которому у одного товара может быть несколько производителей, integer, NOT NULL


### Таблица Products
Таблица содержит информацию о товаре
1. product id - главный ключ таблицы, integer, PRIMARY KEY
2. manufactured item id - внешний ключ, производитель товара, integer, FOREIGN KEY
3. name - наименование товара, varchar, NOT NULL
4. product dealer - внешний ключ, продавец продукта, integer, FOREIGN KEY
5. category name - внешний ключ, имя категории товара, integer, FOREIGN KEY
6. description - описание товара, varchar

### Таблица Product categories
1. category id - - главный ключ таблицы, integer, PRIMARY KEY
2. product category name - наименование  категории, varchar, NOT NULL, UNIQUE

# Возможные Запросы/отчеты/поиски данных
1. Сколько раз купили товар за промежуток времени
2. Какой продавец продал какие товары
3. Какой покупатель купил какие товары
4. У какого продавца есть тот или иной товар
5. К каким категориям отросится товар
6. Какие производители производят определенный товар

# Дополнительные индексы

### Таблица Purchases
```
CREATE INDEX idx_date_col ON purchases (date);
CREATE INDEX idx_product_dealer_col ON purchases(product id, dealer);
CREATE INDEX idx_customer_col ON purchases(customer id);
```
- индекс поиска по временному интервалу ( что бы быстрее делать выборку за нужный период)
- индекс поиска по товарам и продавцам ( для понимания какой продавец продал какие товары)
- индекс поиска по покупателю ( для ускорения поиска истории покупок для покупателя)

### Таблица Products
```
CREATE INDEX idx_manufacture_col ON products (product manufacture);
CREATE INDEX idx_category_col ON products (product category);
```
- индекс поиска по производителю, для ускорения запроса "какие товары производит тот или иной производитель"
- индекс поиска по категории, для ускорения запроса "к какой категории относится товар"


