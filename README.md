# chatbot
serverless, AWS-service-driven Chatbot web application 

## Overview
I will be building an AWS Chatbot using S3, API Gateway, Lambda, Lex, DynamoDB, Elastic Search, and some open source API. 

#### AWS SDK for JavaScript  
[Developer Guide for SDK v2](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/sqs-examples-send-receive-messages.html)

## Workflow 
### step 1
Building chatbot frontend and host it in an AWS S3 bucket. Then set up chat API using AWS API Gateway and connect it with a Lambda function ('chat') to receive and response to chat messages from the user. 
- [x] enable CORS on all API methods including the preflight OPTIONS methods. 
- [x] import the Javascript SDK to the frontend directory to invoke AWS APIs. 

### step 2
Building chatbot using [AWS Lex](https://docs.aws.amazon.com/lex/latest/dg/what-is.html). 

> Amazon Lex is an AWS service for building conversational interfaces for applications using voice and text. With Amazon Lex, the same conversational engine that powers Amazon Alexa is now available to any developer, enabling you to build sophisticated, natural language chatbots into your new and existing applications.

- [x] Created the following three intents: 
1. GreetingIntent
2. ThankYouIntent
3. HotelSuggestionsIntent
Then, set up a lambda function to pass user message to Lex and to receive the processed response from Lex.  

- [x] Through conversation, collect the following pieces of information from the user: 
* Location
* Checkin date
* pet-friendly
* number of nights to stay
* number of beds
* phone number
- [x] fulfillment confirmation: Confirm to the user that you received their request and that you will notify them over SMS once you have the list of hotel suggestions. 

- [x] create another lambda function ('chatbot-backend'). in the fullfillmentCodeHook section, push the information collected from the user to an SQS queue ('myQ'). 

- [ ] Website integration: integrate Lex chatbot into Lambda function 'chat'. Instantiate a 'lex-runtime' client with node.js SDK to establish connection with the bot we just created. 
Note: need to fix problem importing node modules in Lambda....

### step 3 
Use the API to collect 3,000+ hotels in Manhattan and New Jersey. Create a table in DynamoDB to store the collected data. 

### step 4 
Elastic Search

### step 5
set up a queue-worker Lambda function to pull messages from the SQS queue. Generate recommendation of hotel bookings using ElasticSearch and DynamoDB. Send the recommendation through text message using SNS. 
- [x] Lambda queue worker skeleton added
- [x] Set up a scheduler on AWS EventBridge(CloudWatch). Lambda queue worker function will be invoked every one minute. Visibility is tentatively set to 0 for testing purposes. 
- [ ] Set up AWS SNS
- [ ] Build API logic 
