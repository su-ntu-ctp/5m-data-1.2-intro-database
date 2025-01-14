#### Scenario 2

Construct an ER diagram for a school system whose classes have students and teachers. Each student belongs to a single class. Each teacher may teach more than one class, and each class may have more than one teacher.

Each entity has the following attributes:

- Student: id, name, address, phone, email, class_id
- Teacher: id, name, address, phone, email
- Class: id, name, teacher_id

Use the following DBML to create the ERD.

```dbml
Table students {
  id int [pk, increment]
  name varchar
  address varchar
  phone varchar
  email varchar
  class_id int
}

Table teachers {
  id int [pk, increment]
  name varchar
  address varchar
  phone varchar
  email varchar
}

Table classes {
  id int [pk, increment]
  name varchar
  teacher_id int
}

Ref: students.class_id > classes.id // many-to-one

Ref: classes.teacher_id <> teachers.id // many-to-many
```

#### Scenario 3

Construct an ER diagram for a company that sells movies online. The company has a website where customers can browse available movies and place orders. Each order can contain multiple movies.

Use the following DBML to create the ERD.

```dbml
Table customers {
  id int [pk, increment]
  username varchar
  email varchar
  created_at datetime
}

Table movies {
  id int [pk, increment]
  title varchar
  description text
  price int
  created_at datetime
}

Table ecommerce.orders {
  id int [pk, increment]
  customer_id int
  created_at datetime
}

Table ecommerce.order_items {
  id int [pk, increment]
  order_id int
  movie_id int
  quantity int
  created_at datetime
}

Ref: ecommerce.orders.customer_id > customers.id // many-to-one

Ref: ecommerce.order_items.order_id > ecommerce.orders.id // many-to-one

Ref: ecommerce.order_items.movie_id > movies.id // many-to-one
```

#### 3.5.3 Third Normal Form (3NF)

Let's break `Orders` into two tables: `Orders` and `Customers`.

`Orders` table:

| OrderID | CustomerID | OrderDate  |
| ------- | ---------- | ---------- |
| 100     | 1          | 2021-01-01 |
| 200     | 1          | 2021-01-02 |
| 300     | 2          | 2021-01-03 |

`Customers` table:

| CustomerID | CustomerName |
| ---------- | ------------ |
| 1          | John         |
| 2          | Mary         |
