# Section 28 Other Serverless - Step Function 7 AppSync

## 408. Step Function Overview

AWS Step Functions

- Model your workflows as state machines (one per workflow)
 - Order fulfillment, Data processing
 - Web applications, Any workflow
- Written in JSON
- Visualization of the workflow and the execution of the workflow, as well as history
- Start workflow with SDK call, API Gateway, Event Bridge (CloudWatch Event)


Step Function - Task States

- Do some work in your state machine
- Invoke one AWS service
 - Can invoke a Lambda function
 - Run an AWS Batch job
 - Run an ECS task and wait for it to complete
 - Insert an item from DynamoDB
 - Publish message to SNS, SQS
 - Launch another Step Function workflow...

- Run an one Activity
 - EC2, Amazon ECS, on-premises
 - Activities poll the Step functions for work
 - Activities send results back to Step Functions

Step Function - States

- Choice State - Test for a condition to send to a branch (or default branch)
- Fail or Succeed State - Stop execution with failure or success
- Pass State - Simply pass its input to its output or inject some fixed data, without performing work.
- Wait State - Provide a delay for a certain amount of time or until a specified time/date.
- Map State - Dynamically iterate steps.’
- Parallel State - Begin parallel branches of execution.

## 411. Step Functions - Error Handling

Error Handling in Step Functions

- Any state can encounter runtime errors for various reasons:
 - State machine definition issues (for example, no matching rule in a Choice state)
 - Task failures (for example, an exception in a Lambda function)
 - Transient issues (for example, network partition events)

- Use Retry (to retry failed state) and Catch (transition to failure path) in the State Machine to handle the errors instead of inside the Application Code

- Predefined error codes:
 - States.ALL : matches any error name
 - States. Timeout: Task ran longer than TimeoutSeconds or no heartbeat received
 - States. TaskFailed: execution failure
 - States.Permissions: insufficient privileges to execute code

- The state may report is own errors

Step Functions - Retry (Task or Parallel State)

- Evaluated from top to bottom
- ErrorEquals: match a specific kind of error
- IntervalSeconds: initial delay before retrying
- BackoffRate: multiple the delay after each retry
- MaxAttempts: default to 3, set to 0 for never retried
- When max attempts are reached, the Catch kicks in

Step Functions - Catch (Task or Parallel State)

- Evaluated from top to bottom
- ErrorEquals: match a specific kind of error
- Next: State to send to
- ResultPath - A path that determines what input is sent to the state specified in the Next field.

Step Function — ResultPath

- Include the error in the input

## 413. Step Functions - Wait For Task Token

Step Functions — Wait for Task Token

- Allows you to pause Step Functions during a Task until a Task Token is returned
- Task might wait for other AWS services, human approval, 3rd party integration, call legacy systems...
- Append .waitForTaskToken to the Resource field to tell Step Functions to wait for the Task Token to be returned

`
“Resource”: “arn:aws:states:::sqs:sendMessage.waitForTaskToken"
`

- Task will pause until it receives that Task Token back with a Send TaskSuccess or SendTaskFailure API call

## 414. Step Functions - Activity Tasks

Step Functions — Activity Tasks

- Enables you to have the Task work performed by an Activity Worker

- Activity Worker apps can be running on EC2, Lambda, mobile device...

- Activity Worker poll for a Task using GetActivityTask API

- After Activity Worker completes its yore sends a response of tts success/failure using SendTaskSuccess or SendTaskFailure

- To keep the Task active:
 - Configure how long a task can wait by setting TimeoutSeconds
 - Periodically send a heartbeat from your Aye using SendTaskHeartBeat within the time you set in HeartBeatSeconds

- By configurin ape neo and actively sending a heartbeat, Activity Task can wait up to 1 year

## 415. Step Functions - Standard vs Express

Step Functions - Standars vs Express

Step Functions Workflows:

Standard (default):
 - Max. Duration = Up to 1 year
 - Execution Model = Exactly-once Execution
 - Execution Rate = Over 2000 / second
 - Execution History = Up to 90 days or using CloudWatch
 - Pricing = # of State Transitions
 - Use cases = Non-idempotent actions (e.g., processing Payments)

Express:
 - Max. Duration = Up to 5 minutes
 - Execution Rate = Over 100,000 / second
 - Execution History = CloudWatch Logs
 - Pricing = # of executions, duration, and memory consumption
 - Use cases = IOT data ingestion, streaming data, mobile app backends,...

 Asynchronous (At-least once)
 - Doesn't wait for WorkFlow to complete (get results from CW Logs)
 - You don't need an immediate response (e.g., messaging services)
 - Must manage idempotence

 Synchronous (At-most once)
  - You need an immediate response (e.g., orchestrate microservice)
  - Can be invoked from API Gateway or Lambda function