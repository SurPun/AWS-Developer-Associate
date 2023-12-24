# Section 23: AWS Serverless: API Gateway

## 342. API Gateway Overview

AWS API Gateway

- AWS Lambda + API Gateway: No infrastructure to manage
- Support for the WebSocket Protocol
- Handle API versioning (v1, v2...)
- Handle different environments (dey, test, prod...)
- Handle security (Authentication and Authorization)
- Create API keys, handle request throttling
- Swagger / Open API import to quickly define APIs
- Transform and validate requests and responses
- Generate SDK and API specifications
- Cache API responses

API Gateway — Integrations High Level

- Lambda Function
    - Invoke Lambda function
    - Easy way to expose REST API backed by AWS Lambda
- HTTP
    - Expose HTTP endpoints in the backend
    - Example: internal HTTP API on premise, Application Load Balancer...
    - Why? Add rate limiting, caching, user authentications, API keys, etc...
- AWS Service
    - Expose any AWS API through the API Gateway?
    - Example: start an AWS Step Function workflow, post a message to SQS
    - Why? Add authentication, deploy publicly, rate control...

API Gateway - Endpoint Types

- Edge-Optimized (default): For global clients
    - Requests are routed through the CloudFront Edge locations (improves latency)
    - The API Gateway still lives in only one region
- Regional:
    - For clients within the same region
    - Could manually combine with CloudFront (more control over the caching strategies and the distribution)
- Private:
    - Can only be accessed from your VPC using an interface VPC endpoint (ENI)
    - Use a resource policy to define access

API Gateway — Security

- User Authentication through
 - IAM Roles (useful for internal applications)
 - Cognito (identity for external users — example mobile users)
 - Custom Authorizer (your own logic)

- Custom Domain Name HTTPS security through integration with AWS Certificate Manager (ACM)
 - If using Edge-Optimized endpoint, then the certificate must be in us-east- |
 - If using Regional endpoint, the certificate must be in the API Gateway region
 - Must setup CNAME or A-alias record in Route 53

## 344. API Gateway Stages and Deployment

API Gateway — Deployment Stages

- Making changes in the API Gateway does not mean they're effective
- You need to make a "deployment” for them to be in effect
- It's a common source of confusion
- Changes are deployed to “Stages" (as many as you want)
- Use the naming you like for stages (dev, test, prod)
- Each stage has its own configuration parameters
- Stages can be rolled back as a history of deployments is kept

API Gateway — Stage Variables

- Stage variables are like environment variables for API Gateway
- Use them to change often changing configuration values
- They can be used in:
 - Lambda function ARN
 - HTTP Endpoint
 - Parameter mapping templates

- Use cases:
 - Configure HTTP endpoints your stages talk to (dey, test, prod...)
 - Pass configuration parameters to AWS Lambda through mapping templates

- Stage variables are passed to the context’ object in AWS Lambda
- Format: ${stageVariables.variableName}

API Gateway Stage Variables & Lambda Aliases

- We create a stage variable to indicate the corresponding Lambda alias
- Our API gateway will automatically invoke the right Lambda function!

## 345. API Gateway Stages 
 
API Gateway — Canary Deployment

- Possibility to enable canary deployments for any stage (usually prod)
- Choose the % of traffic the canary channel receives
- Metrics & Logs are separate (for better monitoring)
- Possibility to override stage variables for canary
- This is blue / green deployment with AWS Lambda & API Gateway

## 349. API Gateway Integration Types & Mappings

API Gateway - Integration Types

- Integration Type MOCK
 - API Gateway returns a response without sending the request to the backend

- Integration Type HTTP / AWS (Lambda & AWS Services)
 - you must configure both the integration request and integration response
 - Setup data mapping using mapping templates for the request & response

API Gateway - Integration Types

- Integration Type AWS_PROXY (Lambda Proxy):
 - incoming request from the client is the input to Lambda
 - The function is responsible for the logic of request / response
 - No mapping template, headers, query string parameters... are passed as arguments

API Gateway - Integration Types

- Integration Type HT TP_PROXY
 - No mapping template
 - The HTTP request is passed to the backend
 - The HTTP response from the backend is forwarded by API Gateway
 - Possibility to add HTTP Headers if need be (ex: API key)

Mapping Templates (AWS & HTTP Integration)

- Mapping templates can be used to modify request / responses
- Rename / Modify query string parameters
- Modify body content
- Add headers
- Uses Velocity Template Language (VTL): for loop, if etc...
- Filter output results (remove unnecessary data)
- Content-Type can be set to application/json or application xml

Mapping Example: JSON to XML with SOAP

- SOAP API are XML based, whereas REST API are JSON based

Client => RESTful, JSON Payload => API Gateway + Mapping Template => XML Payload => SOAP API

- In this case, API Gateway should:
 - Extract data from the request: either path, payload or header
 - Build SOAP message based on request data (mapping template)
 - Call SOAP service and receive XML response
 - Transform XML response to desired format (like JSON), and respond to the user


## 351. API Gateway Open API

API Gateway - Open API spec

- Common way of defining REST APIs, using API definition as code
- Import existing OpenAPI 3.0 spec to AP! Gateway
 - Method
 - Method Request
 - Integration Request
 - Method Response
 - + AWS extensions for API gateway and setup every single option
- Can export current API as OpenAPI spec
- OpenAPI specs can be written inYAML or JSON
- Using OpenAPI we can generate SDK for our applications

REST API — Request Validation

- You can configure AP! Gateway to perform basic validation of an API request before proceeding with the integration request
- When the validation fails, AP! Gateway immediately fails the request
 - Returns a 400-error response to the caller

- This reduces unnecessary calls to the backend
- Checks:
 - The required request parameters in the URI, query string, and headers of an incoming request are included and non-blank
 - The applicable request payload adheres to the configured JSON Schema request model of the method

REST API — RequestValidation — OpenAPI

- Setup request validation by importing OpenAPI definitions file

## 353. API Gateway Caching

Caching API responses 

- Caching reduces the number of calls made to the backend
- Default TTL (time to live) is 300 seconds (min: Os, max: 3600s)
- Caches are defined per stage
- Possible to override cache settings per method
- Cache encryption option
- Cache capacity between 0.5GB to 237GB
- Cache is expensive, makes sense in production, may not make sense in dev / test

API Gateway Cache Invalidation

- Able to flush the entire cache (invalidate tt) immediately
- Clients can invalidate the cache with header: Cache- Control: max-age=0 (with proper IAM authorization)
- If you don't impose an InvalidateCache policy (or choose the Require authorization check box in the console), any client can invalidate the API cache

