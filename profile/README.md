# Licenta

## Secțiuni UI

- [Acasă](#home)
- [Introducere](#introduction)
- [API](#api) - [Limbaje-de-programare](#api-programming-languages) - [Baze-de-date](#api-databases)
- [Schema Bazei de Date](#database-schema)
- [Testare Performanță API](#api-performance-testing)
  - SQL vs NoSQL
  - C# vs JavaScript vs Python ( SQL )
  - PostgreSQL vs MS SQL Server vs MySQL vs MongoDB

## Limbaje de programare + baze de date

- JavaScript + MongoDB
- JavaScript + PostgreSQL
- C# + MS SQL Server
- Python + MySQL

## Aspecte Măsurabile (5K de cereri pentru 100 de conexiuni simultane)

- RPS (Cereri pe secundă)
- Timpul necesar
- Latență minimă
- Latență medie
- Latență mediană
- Latență maximă
- Latența 25% (25% dintre cereri au fost mai rapide decât acesta)
- Latența 50%
- Latența 75%

### Utilizare Resurse

- Utilizare medie a CPU-ului (%)
- Utilizare medie a memoriei (MB)

## Schema Bazei de Date

### Department

- id: string ( VarChar(255) )
- name: string ( VarChar(255) )
- location: string? ( VarChar(255) )
- employees : Employee[]

### Employee

- id: string ( VarChar(255) )
- firstName: string ( VarChar(255) )
- lastName: string ( VarChar(255) )
- email : string ( VarChar(255) )
- hireDate : dateTime?
- departmentId : string? ( VarChar(255) )
- department : Department?
- orders : Order[]
- projects : Project[]

### Product

- id: string ( VarChar(255) )
- name: string ( VarChar(255) )
- price: decimal ( Decimal(10,2) )
- stockQuantity: int ( Integer )
- orderItems : OrderItem[]

### Order

- id: string ( VarChar(255) )
- customerName: string ( VarChar(255) )
- totalAmount: decimal ( Decimal(10,2) )
- orderItems : OrderItem[]
- employeeId : string ( VarChar(255) )
- employee : Employee

### OrderItem

- id: string ( VarChar(255) )
- quantity: int ( Integer )
- unitPrice: decimal ( Decimal(10,2) )
- orderId : string ( VarChar(255) )
- productId : string ( VarChar(255) )
- order : Order
- product : Product

### Project

- id: string ( VarChar(255) )
- name: string ( VarChar(255) )
- description: string ( Text )
- status: ProjectStatus Enum
- employees : Employee[]

#### ProjectStatus Enum

- NotStarted
- Active
- Inactive
- Completed

#### Data Types Used

- string: VarChar(255)
- dateTime: DateTime
- decimal: Decimal(10,2)
- int: Integer
- text: Text
- enum: Enum

#### One to One Relationships

- Employee -> Department
- OrderItem -> Product
- OrderItem -> Order

#### One to Many Relationships

- Department -> Employee
- Employee -> Order
- Employee -> Project
- Product -> OrderItems
- Order -> OrderItems
- Project -> Employee

#### Many to Many Relationship

- Employee -> Project

## Rute API

- [GET] /departamente - Obține toate departamentele cu angajați (selectează anumite atribute & filtrează după atribute & sortează după atribute & paginează & caută & include entități înrudite & include atributele entităților înrudite)

url: GET /departments?select[selectAttributes]=&filter[name]=&sort[name]=&page[number]=&size[size]=&search[name]=&include[relatedEntities]=

exemplu:

GET /departments?\
select=name,location\
filter[name]=Marketing&filter[location]='Amsterdam'\
sort=-created_at (- descending)\
page=2&size=10\
search=engineering\
include=employees

- [GET] /departamente/:id - Obține un departament după ID cu angajații (selectează anumite atribute & include entități înrudite & include atributele entităților înrudite)

- [POST] /angajați - Creează un nou angajat (validează corpul cererii & include entități înrudite)

- [PUT] /angajați/:id - Actualizează un angajat după ID (validează corpul cererii & include entități înrudite)

- [DELETE] /angajați/:id - Șterge un angajat după ID
