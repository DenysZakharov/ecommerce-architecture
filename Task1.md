# Task 1: New application architecture

## General details
Your team is responsible for developing rules for an e-commerce management application. This rules application will utilize data from e-commerce application and will be responsible for sending notifications or deactivating products within the e-commerce application.
The rules should be based on the following predefined tables :
1. **Products table**
* Product id
* Product name
* Product category
* Status


2. **Sales**
* Sales date
* Product id
* Product cost
* Revenue
* Country
* Payment method
* Payment status

The initial rules you have been asked are the following:
1. If the cost of a product exceeds X USD, and it registers zero sales during the last week,
send an email notification to the e-commerce manager and deactivate the product in the
e-commerce application. This rule applies specifically to laptops and tablets.
2. If the cost of a product is less than X USD and its revenue exceeds Y USD during the
last 2 weeks, send an email notification to the e-commerce manager. However, this rule
should not be applied to printers.
E-commerce managers should be able to customize these rules by specifying parameters such as product categories, cost, sales figures, and time periods. E-commerce manager should be able to add new rules by himself.

## Task
Please provide a design blueprint for a system that answers above requirements. This should include the structure of the database tables, class definitions, and method signatures. We're interested in understanding your architectural approach and how you'd structure the solution, rather than a fully functional implementation.
You can send your solution’s details in the word/PDF document or/and use the git repository. You need to describe the solution , you don’t need to develop a working solution , screens, database etc.
1. **Database Structure**
* Design a database structure that accommodates customizable rules.
* Include necessary indexes to optimize query performance.


2. **Code blueprint with OOP principles**
* Create a code blueprint that includes well-defined classes and their
dependencies.
* Ensure flexibility to accommodate new rules without additional development.
* Describe the key design patterns or principles you intend to make the code easy
to maintain, add new features, and follow established coding standards.


3. **Scalability**
* How will you ensure the application is scalable to accommodate future rule customizations


5. **Estimation**
* Provide a rough estimate for the development effort.
* Specify the resources needed for this task.


7. **Additional aspect**
* What other considerations do you believe are essential for the successful
development and deployment of the customizable rules application?


9. **Solution maintenance and future development**
* Describe a few techniques and managerial routines that will help to ensure the solution stability when new features are implemented.
* How will you ensure that few developers will be able to add new functionalities to the solution independently without blocking each other?
* Describe a few techniques and managerial routines that will ensure cost effectiveness of new features developments
