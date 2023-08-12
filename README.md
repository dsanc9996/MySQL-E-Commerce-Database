# MySQL-E-Commerce-Database
Database created after creating an Entity Relationship model and implemented using MySQL. If you use my code, credit me.


**E-R Model Design**
Establishing Entities
	An E-Commerce Database is a database that focuses on two entities – the customer and the product. Every relationship in the E-R model should incorporate or reference either the product or the customer. The entities of an E-Commerce database are as follows: Customer, Product, Payment, Order, and Shipment (as well as the composite attributes ‘Address’ and ‘Card Info’). 

**Establishing Relationships**
	The relationships between each entity are numerous. The relationships for each entity are as follows:
1.	A customer uses payment to pay for a product. This indicates a ternary relationship between the 3 entities.
2.	Payment is then used to pay for the order. One payment can fulfill multiple orders at a time, indicating a one-to-many relationship. 
3.	The order provides details for the shipment. One shipment can contain many orders, indicating a one-to-many relationship.
4.	A shipment is shipped to a customer. A customer can receive one shipment at a time, indicating a one-to-one relationship.

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/831a6873-0593-4bc3-a6fb-acf9f226b016)

Figure 1 – The ER Model constructed after affirming entities and relationships between entities.
Based on the ER model displayed in Figure 1, 11 tables should be constructed by the time the database is completed.

**Database Construction**
MySQL Commands
  The construction of the ER model allows for the streamlined creation of the database. Below are snapshots and brief explanations of the queries used to construct
  the database, as well as the type of object each table was constructed from using the ER model (Figure 1). 

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/0ed39df6-b838-4b56-8e24-4fc6baa49eb7)

Entity Table – Query used to create entity table ‘customer.’ The primary key was the phone number, as no two people can have the same phone number. VARCHAR was chosen as the data type for all columns because these columns are alphanumeric, or have the potential to be. Three foreign keys were later added from the address composite attribute. They are “houseNumber, zipCode,” and “street.”

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/76bf1103-26e1-4257-896f-387f59581b86)

Composite Attribute Table – Composite attributes make the database easier to navigate. Address is a composite attribute of the customer entity. The primary key is a multicolumn set consisting of “houseNumber, zipCode, street.” This is because no person can have the same exact house number-street-zip code combo.

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/a74c56dc-b0c6-40bc-a493-8e634fd1ffeb)

Entity Table – This entity table centers around the ‘product.’ The product ID was chosen as the primary key, since it is unique. 

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/6e6127e7-506a-41a7-a237-ce68a71f6001)

Entity Table - This entity table centers around the ‘payment.’ The payment ID was chosen as the primary key, since it is unique. This table also references ‘card number’ and ‘cvv’ as its foreign keys to establish a link to the composite attribute ‘cardInfo.’

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/03daeb52-0614-4041-a577-705a4dd5ec4d)

Composite Attribute Table – Composite attribute of the payment entity. A 2 set primary key was chosen, since only one person can have a specific card number – cvv combination. 

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/5188c635-61c8-422c-80fb-0122e677e9c8)

Relationship Table – The purchase table is a ternary relationship that connects ‘payment,’ ‘customer,’ and ‘product.’ This table contains foreign keys that were primary keys of the 3 aforementioned entities. 

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/1aff638e-9831-4686-8fbd-6bf20603809a)

Entity Table – The order info entity is a single domain entity the contains only the order ID. This is to increase security and restrict access to order details.

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/a0f8d535-a929-442d-ab4e-b00d54b887a2)

Relationship Table – The ‘paidOrder’ table is a relationship table that links the ‘orderInfo’ and ‘payment’ entities.

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/231f49e4-ba93-41c3-a0f7-dc8dd6608c2c)

Entity Table - The ‘shipment’ entity is a single domain entity the contains only the tracking number. This is to increase security and restrict access to shipment details.

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/2d2b9af4-1087-4522-98b5-72c6e4eda399)

Relationship Table – The ‘shipmentInfo’ relationship links the ‘shipment’ and ‘orderInfo’ entities to provide more specific order details.

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/3574d2f6-3ba5-422b-a6dd-280c360d1028)

Relationship Table – The ‘delivery’ table is a relationship the links the ‘shipment’ and ‘customer’ tables in order to determine where an order is going and what customer is receiving it. 

All foreign keys in this database system were followed up with “ON CASCADE DELETE” commands to ensure that if parent rows were deleted, then those rows were deleted in child tables.

**Database Manipulation**
Populating Tables (Insert Query)

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/a555131c-3afd-4af0-867b-1581661e1a20)
 
The above query shows the insertion process for all 11 tables in the database. As to not bloat the report, I did not include the 10 other tables’ insertion procedures. All tables received 3 full insertions occupying each distinct column for a total of 33 queries.

**Selection Queries**

Select all customers who placed an order before 2023:

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/c94db8ae-5361-4c42-a81d-0bcad1e9b8a1)

The query above uses a doubly nested query to retrieve customer details about customers who ordered an item before 2023. 

Select the customer whose address was not in San Angelo:

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/ce247a7c-913d-483f-8bc0-cfee9fb21e1f)

By use of another subquery, the customer details of the customer whose address is not in the city of San Angelo was selected. This is verified by the zipCode.

Select the shipping details for every order less than the maximum cost order:

![image](https://github.com/dsanc9996/MySQL-E-Commerce-Database/assets/69611918/aee59249-9e5f-48fb-8b9b-b273438e7814)

The query above selects all shipment details for every order that is less than the maximum cost item from the paidOrder relationship table. Use of a subquery is
required.

**Improvements**
This database suffers from bloat, characteristics can be eliminated from many relationship tables and be moved into entity tables to prevent unnecessary subquery
commands that admittedly get complicated fast. This is all circumvented by clever use of JOIN clauses which I was unable to demonstrate here. Future plans include
improving the ER model and refining the data items found in entities to improve the database performance, integrity, and cohesion.
