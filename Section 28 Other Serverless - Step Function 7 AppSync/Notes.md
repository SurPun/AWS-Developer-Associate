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