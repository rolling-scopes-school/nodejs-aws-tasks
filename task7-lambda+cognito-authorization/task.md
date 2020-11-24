# Task 7 (Lambda Authorizer + Cognito Authorization)

**After Lecture 7 "Lambda Authorizer + Cognito Authorization"**

## Prerequisites
---

- The task is a continuation of **Homework 6** and should be done in the same repo.

## TASK 7.1
---
 
Create a new service, called **authorization-service**, with its own **serverless.yml** file at the same level as product and import services.

The backend project structure should look like:
* backend-repository/product-service
* backend-repository/import-service
* backend-repository/authorization-service
 
Create **basicAuthorizer** lambda function in authorization service in **serverless.yml** file. This lambda should have at least one environment variable with credentials: {yours_github_account_login}=TEST_PASSWORD
* {yours_github_account_login} - your GitHub account name. Login for test user should be your GitHub account name (example: vasiapupkin)
* TEST_PASSWORD - password string. Password for test user must be «TEST_PASSWORD»
 
**basicAuthorizer** lambda should take **Basic authorization_token**, decode it and check that credentials provided by token exist in the lambda environment variable. This lambda should return 403 HTTP status if access is denied for this user (invalid **authorization_token**) and 401 HTTP status in case of other errors.
 
**NOTE:** do not send credentials to the GitHub. Use **.env** file and **serverless-dotenv-plugin** serverless plugin to add environment variables to the lambda. Add **.env** file to **.gitignore** file.

.env file example:
vasiapupkin=TEST_PASSWORD
 
## TASK 7.2
---
 
Add Lambda authorization (**basicAuthorizer** lambda) to the **/import** path of the **import-service** API Gateway.
 
## TASK 7.3
---
 
Request from the client application to the **/import** path of the **import-service** should have Basic Authorization header: 
Authorization: Basic **authorization_token** 
where **authorization_token** is equal base64-encoded({yours_github_account_login}:TEST_PASSWORD)
(For example, Authorization: Basic sGLzdRxvZmw0ZXs0UGFzcw==)
Client should get **authorization_token** value from browser localStorage
 
## Evaluation criteria (each mark includes previous mark criteria)
---

Provide your reviewers with the link to the repo, client application and URLs to execute the **/import** path of the **import-service**

* **1** - **authorization-service** is added to the repo, has correct **basicAuthorizer** lambda and correct **serverless.yaml** file
* **3** - **import-service** serverless.yaml file has authorizer configuration for the **importProductsFile** lambda. Request to the **importProductsFile** lambda should work only with correct **authorization_token** being decoded and checked by **basicAuthorizer** lambda. Response should be in 403 HTTP status if access is denied for this user (invalid **authorization_token**) and in 401 HTTP status if Authorization header is not provided.
* **5** - update client application to send Authorization: Basic **authorization_token** header on import. Client should get **authorization_token** value from browser localStorage https://developer.mozilla.org/ru/docs/Web/API/Window/localStorage
**authorization_token** = localStorage.getItem('**authorization_token**')
 
## Additional (optional) tasks
---
* **+1** - Client application should display alerts for the responses in 401 and 403 HTTP statuses. This behavior should be added to the **nodejs-aws-fe-main/src/index.tsx** file
