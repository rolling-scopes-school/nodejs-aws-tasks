Example task ropository url: https://github.com/angry-coconut/rds-example-task-lesson4

**TASK 4.1**

Use serverless framework to create a database instance in RDS with PostgreSQL and default configuration. 
RDS instance configuration:
...
Connect to database instance via the tool pgAdmin (https://www.pgadmin.org/download) or similar tools like DataGrip/DBeaver and create tables:

    products:
    id -  text (primary key)
    title - text, not null
    description - text
    price - integer

    stocks:
    product_id - integer (foreign key from products.id)
    count - integer

Write SQL script to fill tables with test examples. Store it in your GIT repository. Execute it for your DB to fill data. 


**TASK 4.2**

Extend your serverless.yml file with credentials to your database instance and pass it to lambda’s environment variables section.
Integrate GET/products lambda to return a list of products from the database (joined stocks and products tables)  Product instance on FE side should be joined model of product and stock by productId
 
**Example:**

*BE:*

    Stock example: {
      product_id: 1,
      count: 2
    }
    Product example: {
      price
    }
    
*FE* 

      Product model: {
        product_id: 1,
        count: 2
        price: 123,
        title: ‘Product’,
        description: ‘’
      }

What does it mean for end user - user cannot buy more than product.count (no more items in stock) - But this is future functionality on FE side.
Integrate GET/products/{productId} lambda to return a product from the database

**TASK 4.3**

Implement POST/products lambda and implement its logic so it will be creating a new item in a products table.

You should create a branch from the master and work in the branch (f.e. branch name - task-4) in BE (backend) and in FE (frontend) repository

Provide your reviewers with the link to the repo and URL (API Gateway URL) to execute the implemented lambda functions.

Recommended to use “pg” module to connect the database from the code  https://www.npmjs.com/package/pg.

**EVALUATION CRITERIA:**

Reviewers should verify the lambda functions by invoking them through provided URLs.
 
- **1** - Task 4.1 is implemented, sql script is committed into GIT  (product load into DB)
- **3** - TASK 4.2 is implemented lambda links are provided and return data
- **4** - TASK 4.3 is implemented lambda links are provided and product is stored in DB (call TASK 4.2 to see the product)
- **5** - Your own Frontend application is integrated with product service (/products API) and products from product-service are represented on Frontend. Link to a working Front-End application is provided for cross-check reviewer.


**Additional (optional) tasks (but nice to have):**

- **+1** - POST/products lambda functions returns error 400 status code if product data is invalid
- **+2** - All lambdas return error 500 status code on any error (DB connection, any unhandled error in code)
- **+1** - All lambdas do console.log for each incoming requests and their arguments
- **+1** - Transaction based creation of product  (if stock creation is failed, product is not created and not ready to be used) (TODO: Add more links to it)

