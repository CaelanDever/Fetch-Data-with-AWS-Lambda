<img width="671" alt="4" src="https://github.com/user-attachments/assets/c6992029-c7f0-48e8-8d2a-8959aabd8316" />


# Fetch Data with AWS Lambda

**Author:** Caelan Dever  
**Email:** caelanwd@gmail.com
---

## Introducing Today's Project!

In this project, I will demonstrate the data tier, which is all about how you store and manage the data relevant to your application. I'm doing this project to learn Lambda and DynamoDB.

### Tools and concepts

Services I used were DynamoDB and Lambda. Key concepts I learnt include Lambda functions, DynamoDB set up and IAM permissions. 

### Project reflection

This project took me approximately 53 minutes. The most challenging part was setting up the correct permissions for the Lambda function. It was most rewarding to finally be able to access the DynamoDB with the correct permissions. 

Why did you do this project today? To update my AWS cloud skillset with a focus on DynamoDB and Lambda. Did this project meet your goals? Yes this project exceeded my goals. 

---

## Project Setup

To set up my project, I created a database using DynamoDB. The partition key is the heart of how DynamoDB organizes data which means that it is a label that you can use to group similar items. Under the hood, the partition key is how DynamoDB spread

In my DynamoDB table, I added DynamoDB JSON. DynamoDB is schemaless, which means you can add attributes as you need, and every item in your database can have a different set of attributes. 

<img width="342" alt="53g" src="https://github.com/user-attachments/assets/451ed924-b808-4bd2-ba9e-9d4056b1dc2f" />

### AWS Lambda

AWS Lambda is a service that lets you run code without needing to manage any computers/servers - Lambda will manage them for you. I'm using Lambda in this project to  process data.

---

## AWS Lambda Function

My Lambda function has an execution role, which is an IAM role for your Lambda function. It defines what the function is allowed to do, e.g. accessing other AWS services like DynamoDB. By default, the role grants basic permissions for CloudWatch.

My Lambda function will retrieve data from DynamoDB.

The code uses AWS SDK, which is for JavaScript to interact with DynamoDB. My code uses SDK to use pre-written functions for communicating with DynamoDB and getting data from a table. Without the SDK, you'd have to manually write the code to interact 

<img width="709" alt="4r" src="https://github.com/user-attachments/assets/735d80ed-7026-4c98-9548-72e3c64ebcdc" />


---

## Function Testing

To test whether my Lambda function works, I  send fake events to your function to see how it would react. The test is written in JSON. If the test is successful, I'd see 'Executing function: succeeded'.

The test displayed a 'success' because the function could run but the function's response was actually denied because  we haven't given it explicit permission to access our DynamoDB table. This means DynamoDB is currently blocking the function.


<img width="658" alt="4t" src="https://github.com/user-attachments/assets/3d592326-a382-419a-886f-14a691e86303" />


---

## Function Permissions

To resolve the AccessDenied error we can add a permission policy because it will give us the permissions we're lacking.

There were four DynamoDB permission policies I could choose from, but I didn't pick "AWSLambdaDynamoDBExecutionRole" and "AWSLambdaInvocation-DynamoDB" because they do not allow 'GetItem' permission.

I also didn't pick FullAccess because it lets you do everything with DynamoDB, like creating, deleting, and managing tables. It also lets you read and write data. AmazonDynamoDBReadOnlyAccess was the right choice because it allows 'GetItem'.

<img width="900" alt="3e" src="https://github.com/user-attachments/assets/611395ea-1667-4716-b1c1-7d4615758687" />

---

## Final Testing and Reflection

To validate my new permission settings, I went to the test tab in my Lambda function. The results were successful  because I updated the permissions.

Web apps are a popular use case of using Lambda and DynamoDB. For example, I could help customers find products, get product information or see their order history by fetching data from DynamoDB and help social media apps fetch user profiles.


<img width="671" alt="4" src="https://github.com/user-attachments/assets/d179d04c-f8d5-49ca-9458-97b6c8c2ee74" />



---

## Enhancing Security

For my project extension, I challenged myself to use an inline policy instead of a managed policy like AmazonDynamoDBReadOnlyAccess. This will only allow our Lambda function to access the UserData table, so an inline policy is more secure.

To create the permission policy, I used the visual editor because it's a more beginner friendly, guided interface that breaks up policy writing into checkboxes and dropdowns.

When updating a Lambda funciton's permission policies, you could risk the function permissions getting denied. I validated that my Lambda function still works by back to my Lambda function's Test tab and selecting test again. 

<img width="706" alt="5e" src="https://github.com/user-attachments/assets/324033b4-e21b-4d1b-b8ba-415f3f0adf14" />


---

---
