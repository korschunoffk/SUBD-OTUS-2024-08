## Homework_04
```
mkdir /var/postgres-test && chown -R postgres:postgres /var/postgres-test
```

####DDL
```
CREATE USER kkorshunov WITH PASSWORD '12345678';
CREATE DATABASE homework OWNER kkorshunov;
\c homework;
CREATE SCHEMA shop;
CREATE TABLESPACE shop_homework OWNER kkorshunov LOCATION '/var/postgres-test';

```
```
CREATE TABLE shop.addresses (
	"address id" int NOT NULL,
	"address owner id" int NOT NULL,
	country varchar NOT NULL,
	city varchar NOT NULL,
	street varchar NULL,
	building varchar NULL,
	appartament varchar NULL,
	CONSTRAINT addresses_unique UNIQUE ("address id"),
	CONSTRAINT addresses_pk PRIMARY KEY ("address owner id")
)
TABLESPACE shop_homework

;
```
```
CREATE TABLE shop.phones (
	"phone id" int GENERATED ALWAYS AS IDENTITY NOT NULL,
	"phone owner id" int GENERATED ALWAYS AS IDENTITY NOT NULL,
	"number" varchar NOT NULL,
	"operator" varchar NULL,
	CONSTRAINT phones_unique UNIQUE ("phone id"),
	CONSTRAINT phones_pk PRIMARY KEY ("phone owner id")
)
TABLESPACE shop_homework

;
```
```
CREATE TABLE shop.customers (
	"customer id" int GENERATED ALWAYS AS IDENTITY NOT NULL,
	"name" varchar NULL,
	surname varchar NULL,
	"address owner id" int NULL,
	"phone owner id" int NULL,
	CONSTRAINT customers_pk PRIMARY KEY ("customer id"),
	CONSTRAINT customers_addresses_fk FOREIGN KEY ("address owner id") REFERENCES shop.addresses("address owner id"),
	CONSTRAINT customers_phones_fk FOREIGN KEY ("phone owner id") REFERENCES shop.phones("phone owner id")
)
TABLESPACE shop_homework

;
```
```
CREATE TABLE shop.manufactures (
	"manufacture id" int GENERATED ALWAYS AS IDENTITY NOT NULL,
	name varchar NULL,
	"address owner id" int NULL,
	"phone owner id" int NULL,
	"manufactured item id" int NOT NULL,
	CONSTRAINT manufactures_unique UNIQUE ("manufacture id"),
	CONSTRAINT manufactures_pk PRIMARY KEY ("manufactured item id"),
	CONSTRAINT manufactures_addresses_fk FOREIGN KEY ("address owner id") REFERENCES shop.addresses("address owner id"),
	CONSTRAINT manufactures_phones_fk FOREIGN KEY ("phone owner id") REFERENCES shop.phones("phone owner id")
)
TABLESPACE shop_homework

;
```
```
CREATE TABLE shop."product category" (
	"category id" int GENERATED ALWAYS AS IDENTITY NOT NULL,
	"name" varchar NOT NULL,
	CONSTRAINT product_category_unique UNIQUE ("category id"),
	CONSTRAINT product_category_pk PRIMARY KEY ("category id")
)
TABLESPACE shop_homework

;
```
```
CREATE TABLE shop.dealers (
        "dealer id" int GENERATED ALWAYS AS IDENTITY NOT NULL,
        "name" varchar NOT NULL,
        "phone owner id" int NOT NULL,
        "address owner id" int NULL,
        CONSTRAINT dealers_pk PRIMARY KEY ("dealer id"),
        CONSTRAINT dealers_unique UNIQUE ("name"),
        CONSTRAINT dealers_phones_fk FOREIGN KEY ("phone owner id") REFERENCES shop.phones("phone owner id"),
        CONSTRAINT dealers_addresses_fk FOREIGN KEY ("address owner id") REFERENCES shop.addresses("address owner id")
)
TABLESPACE shop_homework

;
```
```
CREATE TABLE shop.products (
	"product id" int GENERATED ALWAYS AS IDENTITY NOT NULL,
	"name" varchar NOT NULL,
	description varchar NULL,
	"category id" int NOT NULL,
	"dealer id" int NOT NULL,
	"manufactured item id" int NOT NULL,
	CONSTRAINT products_pk PRIMARY KEY ("product id"),
	CONSTRAINT products_product_category_fk FOREIGN KEY ("category id") REFERENCES shop."product category"("category id")
        CONSTRAINT products_dealers_fk FOREIGN KEY ("dealer id") REFERENCES shop.dealers("dealer id");
        CONSTRAINT products_manufactures_fk FOREIGN KEY ("manufactured item id") REFERENCES shop.manufactures("manufactured item id");
)
TABLESPACE shop_homework

;
```
```
CREATE TABLE shop.prices (
	"price id" int NOT NULL,
	price int NOT NULL,
	currency varchar NOT NULL,
	CONSTRAINT prices_pk PRIMARY KEY ("price id"),
	CONSTRAINT prices_unique UNIQUE (currency)
)
TABLESPACE shop_homework

;
```
```
CREATE TABLE shop.purchases (
	"purchase id" int NOT NULL,
	"product id" int NULL,
	"dealer id" int NULL,
	"price id" int NULL,
	"customer id" int NULL,
	"date" date NOT NULL,
	CONSTRAINT purchases_pk PRIMARY KEY ("purchase id"),
	CONSTRAINT purchases_customers_fk FOREIGN KEY ("customer id") REFERENCES shop.customers("customer id"),
	CONSTRAINT purchases_products_fk FOREIGN KEY ("product id") REFERENCES shop.products("product id"),
	CONSTRAINT purchases_prices_fk FOREIGN KEY ("price id") REFERENCES shop.prices("price id"),
	CONSTRAINT purchases_customers_fk_1 FOREIGN KEY ("customer id") REFERENCES shop.customers("customer id")
)
TABLESPACE shop_homework

;
```
