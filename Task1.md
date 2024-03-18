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
Please provide a design blueprint for a system that answers the above requirements. This should include the structure of the database tables, class definitions, and method signatures.
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


4. **Estimation**
* Provide a rough estimate for the development effort.
* Specify the resources needed for this task.


5. **Additional aspect**
* What other considerations do you believe are essential for the successful
development and deployment of the customizable rules application?


6. **Solution maintenance and future development**
* Describe a few techniques and managerial routines that will help to ensure the solution stability when new features are implemented.
* How will you ensure that few developers will be able to add new functionalities to the solution independently without blocking each other?
* Describe a few techniques and managerial routines that will ensure cost effectiveness of new features developments


## Solution
1.  **Database Structure**
```sql
CREATE TABLE Products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    product_category VARCHAR(50),
    status VARCHAR(20)
);

CREATE TABLE Sales (
    sales_id INT PRIMARY KEY,
    sales_date DATE,
    product_id INT,
    product_cost DECIMAL(10, 2),
    revenue DECIMAL(10, 2),
    country[^1] VARCHAR(50),
    payment_method VARCHAR(50),
    payment_status VARCHAR(20),
    INDEX (product_cost),
    INDEX (sales_date)
);

CREATE TABLE Rules (
    rule_id INT PRIMARY KEY,
    rule_name VARCHAR(100),
    condition TEXT,
    action TEXT,
    parameters TEXT,
    is_active BOOL
);

[^1]: probably if we need country codes alpha-2/3 it will be extra table `Countries`
```

2. **Code blueprint with OOP principles**

   **Note**: used `phpcs`, `phpmd` etc.
```php
<?php
class Product {
    public function __construct(
        protected int $product_id,
        protected string $product_name,
        protected string $product_category,
        protected string $status
    ) {}

    // Getters and setters
}

class Sales {
    public function __construct(
        protected int $sales_id,
        protected string $sales_date,
        protected int $product_id,
        protected float $product_cost,
        protected float $revenue,
        protected string $country,
        protected string $payment_method,
        protected string $payment_status
    ) {}

    // Getters and setters
}

class Rule {
    public function __construct(
        protected int $rule_id,
        protected string $rule_name,
        protected string $condition,
        protected string $action,
        protected string $parameters
    ) {}

    // Getters and setters

    public function applyRule(Product $product, array $salesData): void {
        if ($this->evaluateCondition($product, $salesData)) {
            $this->performAction($product);
        }
    }

    private function evaluateCondition(Product $product, array $salesData): bool {
        // Implement condition evaluation logic
        // For rule 1: If cost exceeds X and zero sales during last week
        // For rule 2: If cost less than X and revenue exceeds Y during last 2 weeks
        return true; // Placeholder for condition evaluation
    }

    private function performAction(Product $product): void {
        // Implement action logic
        // For rule 1: Send email notification and deactivate product
        // For rule 2: Send email notification
    }
}
?>

```
**Classes:**
* `RuleManager`: Responsible for managing customizable rules.
* `NotificationService`: Handles email notifications.
* `ProductService`: Manages products and their status.
* `SalesService`: Manages sales data retrieval and processing.

**Dependencies:**
* `RuleManager` depends on ProductService and NotificationService.
* `ProductService` interacts with the database to retrieve and update product information.
* `NotificationService` sends email notifications.

**Design Patterns/Principles**
* `Factory Method Pattern`: Use this pattern to create instances of Rule objects based on certain criteria.
* `Observer Pattern`: Implement this pattern to notify the e-commerce manager when certain conditions are met.
* `Dependency Injection`: Use DI to inject dependencies into classes, making them more modular and easier to test.
* `Repository Pattern`: Implement this pattern to separate data access logic from business logic, improving maintainability and testability.



3. **Scalability**
* Use a modular architecture allowing easy addition of new rules without modifying the core codebase.
* Implement a plugin system where new rules can be added as separate modules. For example, each rule can be implemented as a separate PHP class that follows a common interface, and the system can dynamically load and execute these classes based on the rules configured in the database.
* Utilize caching mechanisms to improve performance, especially for frequently accessed data.


4. **Estimation**
Development effort depends on the complexity of rules, customization options, and integration requirements. Roughly, it could take several weeks to a few months for development. Resources needed would include PHP developers, DevOps, and potentially a project manager for coordination.
* **Development Effort**: Approximately 40-60 hours for initial development.
* **Resources**: Developers (2-3): Backend developers proficient in database design and PHP code.



5. **Additional aspect**
* **Security**: Implement authentication and authorization mechanisms to ensure only authorized users can modify rules.
* **Logging**: Implement logging mechanisms to track rule modifications and system events for auditing purposes.
* **Testing**: Implement comprehensive unit tests to ensure rule evaluation and action execution are working correctly.



6. **Solution maintenance and future development**
* **Version Control**: Use Git for version control to manage changes and updates.
* **Code Review**: Implement a code review process to ensure code quality and prevent conflicts.
* **Continuous Integration/Continuous Deployment (CI/CD)**: Set up CI/CD pipelines to automate testing and deployment processes for new features.
* **Documentation**: Maintain comprehensive documentation to facilitate knowledge transfer and onboarding of new developers.
* **Agile Methodologies**: Adopt agile methodologies like Scrum or Kanban for iterative development and efficient project management.
* **Technical Debt Management**: Regularly address technical debt to maintain code quality and prevent future development bottlenecks.

### Conclusion
This architecture provides a solid foundation for the development of a customizable rules application for e-commerce management. By following established coding standards, design patterns, and scalability principles, the solution can be easily maintained, extended, and scaled to meet future requirements.
