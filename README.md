# MIST4610GroupProject2

## MIST 4610: Group Project 2 Information
 
# Team name and members:
Include information about the name of the team, the names of all team members as well as links to their corresponding GitHub repos that have the project on them.
Giovanna Palma - @gpalma77 
Katie Witcher - @katiewitcher
Jack Macken-
Andrew Baich -
Brooke Istishin - @brookeistishin 
Scenario description:
Our project models a small, local coffee shop chain in Georgia, operating multiple locations under unique names, but all managed centrally with a unified menu. The owner oversees all locations using a central data center to streamline operations.
Key entities in the database include Customer, LoyaltyProgram, Order, Employee, Coffee Shop, OrderItem, MenuItem, RecipeItem, Ingredients, Supplier, Address, and Category. These entities and their relationships allow the database to efficiently track customer visits, the details of their orders, payment methods, and the employee handling each transaction at a specific location. Additionally, the database stores information on the menu items ordered, their ingredients, and the corresponding recipes. It also manages stock levels and tracks suppliers for each ingredient, ensuring a seamless supply chain.
 
# Data Model:
Each customer is uniquely identified and can place multiple orders over time. There is a one-to-many relationship between the Customer and Order entities, meaning that a customer can make many orders, but an order is linked to only one customer. Customers also have a one to one relationship with LoyaltyProgram, as each customer can have up to one account and each account is associated with one customer. The loyalty program keeps track of things like join date, status, points (they earn 1 point for every $ spent, and can use 100 points to redeem a free drink), and additionally their favorite menu item (as a foreign key from menu) and flavor (as a foreign key from ingredient). 
Orders capture the details of a customer’s purchase, including the date of the order and the amount of points a customer who is in the loyalty program will gain. Each order is associated with one customer and one employee, reflecting that the order is processed by a specific employee at a given coffee shop. However, each employee can handle multiple orders, creating a one-to-many relationship between the Employee and Order entities.
Employees are linked to a specific coffee shop location and are responsible for handling customer orders. There is a one-to-many relationship between the CoffeeShop and Employee entities, indicating that a coffee shop can have multiple employees, but each employee works at only one coffee shop. Additionally, each employee has a boss, represented by a one-to-many recursive relationship where one employee can manage several others.
Each coffee shop location is uniquely identified and operates under a unified menu system. There are five coffee shops: Witcher Brew, Andrew's Affogato, Brooke Beanery, Gio's Grind House, and Macken Macchiato. Coffee Shop has a one-to-one relationship with the Employee entity as one employee is the boss of one store, and each store only has one employee as the boss (store manager).Coffee Shop also has a one-to-many relationship with the Ingredients entity as a coffee shop can hold inventory of multiple ingredients but a specific ingredient is only held at one store. 
 Orders often contain multiple menu items, such as different types of coffees or pastries. The OrderItem entity acts as a weak entity between Order and MenuItem, capturing the details of which menu items were included in each order and in what quantity. An order can contain many menu items, and a menu item can be included in multiple orders, making OrderItem an associative entity.
Menu items represent the products sold by the coffee shops, such as different types of drinks or food. Each menu item belongs to one category, such as "Breakfast”. There is a one-to-many relationship between the Category and MenuItem entities, meaning that a category can contain many menu items, but a menu item belongs to only one category.
The RecipeItem entity details the ingredients required to create each menu item. A single menu item can require multiple ingredients, such as coffee, sugar, or milk, while the same ingredient can be used in many different menu items. This is represented by the many-to-many relationship between MenuItem and Ingredient.
Ingredients represent the raw materials needed to prepare menu items. There is a one-to-many relationship between the Supplier and Ingredient entities, meaning that a supplier can provide multiple ingredients, but each ingredient is sourced from only one supplier.
Suppliers provide the ingredients required to prepare the coffee shop’s menu items. Each supplier can supply multiple ingredients to different coffee shop locations, ensuring a steady flow of stock to maintain operations.
A new entity to our model is Address, an associate entity that stores the addresses for 
coffee shops, suppliers, employees, and customers. There is a one to one relationship for 
 Coffee shops and suppliers as they cannot have more than one address and are not a place of residency. Employees and customers have a one to many relationship since there is a possible situation where an address can have many residents. 

 
# Data Model Changes from Project 1:
Customer Table
•	email VARCHAR(45) in the earlier model is now updated to VARCHAR(100) for better compatibility with longer email addresses.
Order Table
•	Added a Points field (INT) to track points associated with orders.
•	Changed totalAmount to DECIMAL(5,2) for precision in financial data.
Employee Table
•	Salary is now appropriately scaled (DECIMAL(6,2)).
Ingredients Table
•	stockQty was changed from INT to DECIMAL(10,2) to account for fractional quantities (e.g., partial kilograms or liters).
LoyaltyProgram Table
•	The earlier model does not include the LoyaltyProgram table in the diagram. In the revised model, it tracks Customer_idCustomer, joinDate, Status, and Points.
•	Loyalty program is identified by a customer id. It is optional for customers to be enrolled in the program. They earn points on each dollar of each order they make, and can pay with 100 points for 1 drink.
RecipeItem Table
•	IngredientAmount is (DECIMAL(5,2))
Address Management
•	New aggregate entity that tracks addresses.
•	In the earlier model, addresses were directly linked to entities like Customer, CoffeeShop, and Supplier. 




# Data Dictionary:
  

 















 
 



 


 



 




# Five Queries:

Query 1 
This query returns the 5 lowest stock quantities of ingredients and in which restaurant the low stock occurs. In addition, the query highlights the number of recipes the low ingredient is used in the restaurant. A left join is used to show if the quantity of the items on the menu is zero, then we do not need to restock. This query is helpful because we want to prioritize which of our ingredients we need to restock based on how often they are used.

 

Query 2 (most popular menu items ordered together)
Can see market trends of popular menu items
Can allow the creation of discounted pairings that will be ordered
Can help the creation of new menu items based on the relationship of the food ordered together
 

Query 3 (this query shows the top 10 customers who are gold reward members and how much revenue they have brought to the business) can be used to compare if they spend more than customers who are not rewards member, etc.
 


Query 4 
This query reports the number of customers who have ordered at each coffee shop location more than once. The output can indicate coffee shop locations’ customer retention rates and successful practices. Managers could use this information to assess the effectiveness of loyalty and rewards program marketing at the different locations, customer experience, and regional strategies. For managers, this information will be useful when optimizing resource allocation, identifying regional trends, and strengthening the chain's competitive advantage. 

 















Query 5
This query shows the total revenue for each month in 2023. For managers, this information is highly useful to identify possible patterns and changes in revenue categorized by seasonal spending changes by consumers. This information could be helpful when crafting revenue predictions, assessing benchmarks, and goal setting for future months and years. Overall, tracking revenue is vital to determine the health of a business by assessing operating margin, cash flow, and overall liquidity. 

 












# Tableau Visualizations

#1 
 

This visual showcases the most commonly ordered flavors among loyalty customers. The x-axis is the name of the flavor, and the y-axis is the number of times the flavor is ordered by Loyalty Customers. This visualisation is important for management because any customer information can improve inventory and marketing efforts. Incentives can be put in place that reward Loyalty Customers with top flavors, and stores should put extra emphasis to have plenty of these flavors in stock. In addition, the sample size of Loyalty Customers is a good sample for the population of all customers, further adding value via customer data. 

#2
 
This visual focuses on the total quantity each food item is ordered, a very important metric for management to see which of its foods are a hit among customers and which are not as popular. With this information, management can make pricing and marketing decisions, as well as better inventory management. Successful marketing and customer relations often revolve around knowing the customer, and information on consumer habits helps any brand put the customer first.

#3
 

This visualization breaks down the total revenue from each store. With this visual, it is easy to compare which stores are outperforming others and by how much. Important conclusions can be made from this model, such as which stores are finding top line success while which are struggling, and which stores have hit their sales goal. In addition, management can gauge its total revenue and make projections for future performance.










#4
 

The dashboard above showcases all the visuals together to create a hub for analysis and effective conclusions. In addition to the bar graphs, in the top right corner, there is a line graph that  highlights the quantity of orders each coffee shop has had from 2020-2019. The graph provides a visual for an important metric in the restaurant industry- how many orders are being placed at each location. With this visual, trends are easily identifiable to illuminate which stores are increasing order volume and which are not. For example, Brooke’s Beanery has been steadily increasing order volume, while Witcher Brew has been struggling. With this data, conclusions can be drawn about shop performance and future expenditures. Management must determine what factors have led to Witcher Brew’s performance decline and how they can be fixed. 

# Database information:
Name of database: cs_gcp90285

Additional information: Each Each query listed above is marked in the database using stored procedures which can be called using the following format: CALL Q1();
