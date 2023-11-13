# База данных для хранения информации о товарах в  магазине бытовой  техники.


# Структура базы данных "StoreDB"

## Таблица "Categories"

| Название поля | Тип поля      | Описание поля                                                   |
|---------------|--------------|----------------------------------------------------------------|
| CategoryID    | INT          | Уникальный счетчик для определения записи в таблице             |
| CategoryName  | NVARCHAR(50) | NOT NULL; поле для ввода названий категорий                      |

## Таблица "Suppliers"

| Название поля | Тип поля      | Описание поля                                                   |
|---------------|--------------|----------------------------------------------------------------|
| SupplierID    | INT          | Уникальный счетчик для определения записи в таблице             |
| SupplierName  | NVARCHAR(50) | NOT NULL; поле для ввода названия поставщика                    |
| ContactName   | NVARCHAR(50) | NOT NULL; поле для ввода контактного лица                       |
| Phone         | NVARCHAR(20) | NOT NULL; поле для ввода имени контактного лица поставщика      |
| Email         | NVARCHAR(50) | NOT NULL; поле для ввода электронной почты поставщика           |

## Таблица "Products"

| Название поля | Тип поля      | Описание поля                                                   |
|---------------|--------------|----------------------------------------------------------------|
| ProductID     | INT          | Уникальный счетчик для определения записи в таблице             |
| ProductName   | NVARCHAR(100)| NOT NULL; поле для ввода названия товара                        |
| CategoryID    | INT          | NOT NULL; внешний ключ для связи с таблицей Categories          |
| SupplierID    | INT          | NOT NULL; внешний ключ для связи с таблицей Suppliers           |
| Price         | NVARCHAR(200)| NOT NULL; поле для ввода цены товара                             |
| StockQuantity | INT          | NOT NULL; поле для ввода количества товаров на складе           |


```sql

CREATE TABLE Categories (
    CategoryID INT PRIMARY KEY,
    CategoryName NVARCHAR(50) NOT NULL
);

CREATE TABLE Suppliers (
    SupplierID INT PRIMARY KEY,
    SupplierName NVARCHAR(50) NOT NULL,
    ContactName NVARCHAR(50),
    Phone NVARCHAR(20),
    Email NVARCHAR(50)
);

CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(100) NOT NULL,
    CategoryID INT,
    SupplierID INT,
    Price DECIMAL(10, 2) NOT NULL,
    StockQuantity INT NOT NULL,
    CONSTRAINT FK_Products_Category FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID),
    CONSTRAINT FK_Products_Supplier FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID)
);

