# ABOUT TERRAFORM FILE

# SNS

- fifo_topic = false, helps us to Publish message to lambda successfully. This type is called standard
SNS, with FIFO type we cannot Publish message to lambda successfully.
- subscription resource is needed to link lambda to publish message to it.

# LAMBDA

- IAM Role with trust relationship with lambda is created
- For actual function, filename is the zip file which has lambda function code
and handler is the python file name which will handle the event. The runtime is python 3.8 
because we have a python lambda function
- IAM policy to log data from lambda to cloudwatch and put object to DynamoDB is needed.
I added policy code from CloudWatchFullAccess and AmazonDynamoDBFullAccess.
- In policy attachment resource, attached the policy to IAM role created above.
- This step is very important, else our lambda won’t be able to fetch data from SNS.
Resource aws_lambda_permission is needed to link things from lambda side.
Else we will be able to add lambda in Subscriptions to SNS, but trigger link will be missing.

# DYNAMODB

- Hash_key is partition key
range key is sort_key

