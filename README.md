My solution
====
My solution is a REST API build on top of **AWS API Gateway & AWS Lambda & DynamoDB.**

Reasons I chose these technologies:
1. **Pay per use**: using microservices it's not necessary to pay for a 24h-running server, you only pay for each invocation of your service. These prices are very cheap and included in the AWS Free tier.
0. **Scales automatically**: API Gateway and Lambda scales in an automated way so it works perfectly for a single user or for millons of them.
0. **No infrastructure maintenance**: working with serverless architectures, there is no servers to maintain/path/update. AWS takes cares of all these topics in a managed way.
0. **Easy caching**: It's pretty simple to enable some cache policies for any method in my API.
I asumed there is no need to secure my service so I do not add any key tokens in my Gateway API.

**User story 1:**

For this case I used an **API Gateway** endpoint that interacts directly with a simple Lambda function *SaveExpenseFunction*. API gateway url /expenses - method POST.
This is another reason I choose  API Gateway, I can decide where/how are handled any defined method in my API.
I used DynamoDB Java annotations in order to simplify my db-object mapper.
I wrote many jUnit tests in the lambda-java project.
I used a fictional employee (challenge-employee) related to all the expenses the app creates. The main index in the table is employee askey and expenseId as range sort. I thought it's a eficient way to retrive only the employee expenses in the case there were many employees.

**User story 2:**

This user story is quite simple so it's posible to achieve **without code**. AWS API Gateway have some managed integrations througth others AWS resources (DynamoDB included). I wrote a simple mapping response/request template in order to adapt the front-end request to DynamoDB API methods and viceversa.
I used here the same fictional employee.

You can test these GET endpoint of the api using POSTMAN o curl directly.
My endpoint: https://sxxumq090h.execute-api.eu-west-1.amazonaws.com/prod/expenses

**User story 3:**

I've created a service *ExchangeRateService* that cares about currencies exchanges. Have wrote some jUnit tests but it's not fully integrated in my solution.

**User story 4:**

I've made some changes in the front but not tested so much. Now VAT can be filled directly for each user

Others solutions
====
Java EE project (using maven) with Spring MVC & Hibernate | JPA would be a good choice for me. It could be scaled easely placing the war inside a server behind a load balancer or inside a docker/tomcat|jetty.
I discarded these solution because of the serverless API advantages. IMO offers better performance results and it's easier to maintain and test.
 
