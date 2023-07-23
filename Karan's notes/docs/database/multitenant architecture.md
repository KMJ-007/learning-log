what is multi tenancy in database architecture ?

like there are ways how you can organise your data in your relational database

first and simplest approach is to put all the data in one single table and introduce the new column as new need them,

but in this after sometime you face that, this method works for simple data, but when you have relations between data, this approach is not so useful because, it will create duplicate data, you are storing same thing again and again,

so to overcome that you now split your data and store them in the different table according to relations, you have users data and their orders, let's say, so for user's data you will have one different table and for order's data you will have different table, you will create a simple relation between user and order, so you can fetch/query the orders of specific users,

but in this 