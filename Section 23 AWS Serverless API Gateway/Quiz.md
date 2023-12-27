# Quiz 20: API Gaetway Quiz

1. To make a Serverless API, you should integrate API Gateway with ......................

- AWS Lambda

2. To redirect your API Gateway stage to the correct AWS Lambda Alias, you should use .........................

- Stage Variables

3. You can integrate API Gateway with the following, EXCEPT ....................

- AWS CloudShell

4. You have created a whole new API (v2) and you want to test it, but you're worried about shifting all the traffic to it. What is the recommended way to test it?

- Create a Canary release

5. You have an API Gateway backed by a set of Lambda functions and you want to mask some fields in the output data returned by one of the Lambda functions. What should you use?

- Mapping Templates

6. Which specification allows you to import/export your API as code?

- Swagger / OpenAPI

7. You are running an API that's backed by a Lambda function. Your API receives a large number of GET requests which results in your Lambda function becomes overloaded and your bill starts to substantially increase. The response returns the same payload and changes once each day. What should you do to handle all these requests and reduce your bill?

- Enable Caching for your Stage

8. API Gateway Caching is defined per ..................... with the default TTL .....................

- Stage, 300 seconds

9. How can clients invalidate the cache of an API from the client-side?

- Pass the HTTP header `Cache-Control: max-age=0`

10. You are serving a Machine Learning API through API Gateway to a number of customers that they're using in their applications. You offer this as a free service, but you plan to purchase each customer with paid plans. Which API Gateway feature allows you to do so?

- Usage Plans & API Keys

11. You have a Serverless application consists of an API Gateway, Lambda functions, and DynamoDB tables. Lately, users begin to complain that they receive exceptions in some requests. Also, there's a delay in some API calls. What should you use to troubleshoot and detect where the issues take place?

- X-Ray

12. You have an API that's consumed by a large number of users from different domains. You need to ....................

- Enable CORS

13. You want to authenticate requests made to your API. All requests contain a Bearer token provided in the Authorization HTTP header. These tokens must be validated against a 3rd party provider. What should you use?

- API Gateway Lambda Authorizer

14. You would like to authenticate your users against Facebook before they are able to make requests to your API hosted by API Gateway. What should you use to make a seamless authentication integration?

- Cognito User Pools

15. Which of the following HTTP error code API Gateway returns where there are too many requests?

- 429

16. Which of the following CloudWatch metrics helps you analyze the timeout issues between your API Gateway and a Lambda function?

- IntegrationLatency

17. API Gateway supports the WebSocket protocol for real-time APIs.

- True