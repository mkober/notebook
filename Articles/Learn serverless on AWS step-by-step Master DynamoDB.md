Clipped from: [https://dev.to/slsbytheodo/learn-serverless-on-aws-step-by-step-master-dynamodb-3cki](https://dev.to/slsbytheodo/learn-serverless-on-aws-step-by-step-master-dynamodb-3cki)

## TL;DR

In this [series](https://dev.to/pchol22/series/22030), I try to explain the basics of serverless on AWS, to enable you to build your own serverless applications. During [last article](https://dev.to/slsbytheodo/learn-serverless-on-aws-step-by-step-strong-types-213i), I showed you how to use contracts to use [🐝 swarmion 🐝](https://github.com/swarmion/swarmion) to create Lambda functions easily and type them strongly. Today, let's continue with the same idea to improve our developer experience with DynamoDB!

I already wrote an article that is [an introduction to DynamoDB](https://dev.to/slsbytheodo/learn-serverless-on-aws-step-by-step-databases-kkg). If you go and read it, you will quickly see that while being a great database, DynamoDB is painful to use in Lambda functions: items have a weird format, are not typed and building commands like queries does not feel natural. In this article, follow me through the process of improving our code step by step!

[Follow me on twitter 🚀](https://twitter.com/PierreChollet22)

### What will we do today?

- Create two very simple Lambda functions: createUser and listUsers, using the classic DynamoDB SDK

- Users type will be : { username: string; email: string; age: number; adult: boolean }

- Replace the DynamoDB SDK with the DocumentClient SDK, to get rid of the weird .S .N .BOOL ... format
- Replace the DocumentClient SDK with [dynamodb-toolbox](https://www.dynamodbtoolbox.com/), to get a more natural API and strongly typed queries

If you have difficulties to follow, you can find the code at the end of the article [here](https://github.com/PChol22/learn-serverless-ddb-toolbox).

Quick announcement: I also work on a library called [🛡 sls-mentor 🛡](https://www.sls-mentor.dev/). It is a compilation of 30 serverless best-practices, that are automatically checked on your AWS serverless projects (no matter the framework). It is free and open source, feel free to check it out!

[Find sls-mentor on Github ⭐️](https://github.com/sls-mentor/sls-mentor)

## The classic (and painful) DynamoDB experience

### Setting up a DynamoDB table and Lambda functions

Like all the articles of this [series](https://dev.to/pchol22/series/22030), we will use the AWS CDK with Typescript to create our infrastructure. If you are not familiar with it, go back to my [first article](https://dev.to/slsbytheodo/dont-miss-on-the-cloud-revolution-learn-serverless-on-aws-the-right-way-1kac) to learn how to get started.

First, let's start by writing the Infrastructure as code in the CDK stack. We will create a DynamoDB table, an API and two Lambda functions, while not forgetting to give the right permissions and environment variables to the Lambda functions to access the DynamoDB table.  
 

import * as cdk from 'aws-cdk-lib';  
import { Construct } from 'constructs';  
import { join } from 'path';  
  
// Use the Node18 runtime which provides the aws-sdk v3 natively  
// This way our Lambda functions bundles will be smaller  
const sharedLambdaConfig = {  
  runtime: cdk.aws_lambda.Runtime.NODEJS_18_X,  
  bundling: {  
    externalModules: ['@aws-sdk'],  
  },  
};  
  
export class BackendStack extends cdk.Stack {  
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {  
    super(scope, id, props);  
  
    const api = new cdk.aws_apigateway.RestApi(this, 'Api', {});  
  
    const table = new cdk.aws_dynamodb.Table(this, 'DdbTable', {  
      partitionKey: { name: 'PK', type: cdk.aws_dynamodb.AttributeType.STRING },  
      sortKey: { name: 'SK', type: cdk.aws_dynamodb.AttributeType.STRING },  
      billingMode: cdk.aws_dynamodb.BillingMode.PAY_PER_REQUEST,  
    });  
  
    const classicRoute = api.root.addResource('classic');  
  
    const classicCreateUser = new cdk.aws_lambda_nodejs.NodejsFunction(this, 'ClassicCreateUser', {  
      entry: join(__dirname, 'classic.ts'),  
      handler: 'createUser',  
      environment: {  
        TABLE_NAME: table.tableName,  
      },  
      ...sharedLambdaConfig,  
    });  
    table.grantWriteData(classicCreateUser);  
    classicRoute.addMethod('POST', new cdk.aws_apigateway.LambdaIntegration(classicCreateUser));  
  
    const classicListUsers = new cdk.aws_lambda_nodejs.NodejsFunction(this, 'ClassicListUsers', {  
      entry: join(__dirname, 'classic.ts'),  
      handler: 'listUsers',  
      environment: {  
        TABLE_NAME: table.tableName,  
      },  
      ...sharedLambdaConfig,  
    });  
    table.grantReadData(classicListUsers);  
    classicRoute.addMethod('GET', new cdk.aws_apigateway.LambdaIntegration(classicListUsers));  
  }  
}  
 

The NodeJsFunction construct requires esbuild to be installed in your project -> npm i -D esbuild

Compared with my previous articles, nothing really new here! The only new improvement is the clever use of the Node18 runtime, which provides the aws-sdk v3 natively. This way, we don't need to bundle the aws-sdk in our Lambda functions, which makes them smaller. We do this by specifying the externalModules option in the bundling property of the NodeJsFunction construct.

### The classic DynamoDB Lambda function code

Based on the IAC we just created, we have to create a file named classic.ts in the same directory as the stack, and write the code of the lambda handlers inside. Using the classic DynamoDB SDK, it looks like this:  
 

import { DynamoDBClient, PutItemCommand, QueryCommand } from '@aws-sdk/client-dynamodb';  
  
const ddbClient = new DynamoDBClient({});  
const tableName = process.env.TABLE_NAME ?? '';  
  
export const createUser = async (event: { body: string }) => {  
  const { username, email, age, adult } = JSON.parse(event.body) as {  
    username: string;  
    email: string;  
    age: number;  
    adult: boolean;  
  };  
  
  await ddbClient.send(  
    new PutItemCommand({  
      TableName: tableName,  
      Item: {  
        PK: { S: 'USER' },  
        SK: { S: username },  
        email: { S: email },  
        age: { N: age.toString() },  
        adult: { BOOL: adult },  
      },  
    }),  
  );  
  
  return {  
    statusCode: 200,  
    body: JSON.stringify({  
      message: 'User created successfully',  
    }),  
  };  
};  
  
export const listUsers = async () => {  
  const { Items = [] } = await ddbClient.send(  
    new QueryCommand({  
      TableName: tableName,  
      KeyConditionExpression: 'PK = :pk',  
      ExpressionAttributeValues: {  
        ':pk': { S: 'USER' },  
      },  
    }),  
  );  
  
  return {  
    statusCode: 200,  
    body: JSON.stringify({  
      users: Items.map(user => ({  
        username: user.SK.S,  
        email: user.email.S,  
        age: +(user.age.N ?? '0'),  
        adult: user.adult.BOOL ?? false,  
      })),  
    }),  
  };  
};  
 

If you read my [first dynamodb article](https://dev.to/slsbytheodo/learn-serverless-on-aws-step-by-step-databases-kkg), you will recognize the same structure. We create a DynamoDBClient and use it to send commands to DynamoDB.

- CreateUser: We have to be cautious to use the .N .S .BOOL format to interact with DynamoDB, to represent string, number and boolean attributes. This is not very natural and can be confusing.
- ListUser: We must use the KeyConditionExpression and ExpressionAttributeValues properties to setup our query. This is also quite painful!

Furthermore, we have to autocompletion and type safety when writing our code! This is OK in small projects, but can quickly become a nightmare in bigger projects.

But don't worry, I got you covered! First, let's replace the DynamoDB SDK with the DocumentClient SDK to get rid of the .N .S .BOOL format.

## Using DocumentClient instead of the classic DynamoDB SDK

The DocumentClient SDK is another SDK developed by AWS. Basically, it is a wrapper around the classic DynamoDB SDK, which automatically marshalls and unmarshalls (serializes and deserializes) the data for you. This way, you don't have to use the .N .S .BOOL format anymore, and you can use the native types of your programming language.

### Create two new Lambda functions

First, let's add two new Lambda functions to the IAC of the project in our CDK stack:  
 

// ... previous code  
const documentRoute = api.root.addResource('document');  
  
const documentCreateUser = new cdk.aws_lambda_nodejs.NodejsFunction(this, 'DocumentCreateUser', {  
  entry: join(__dirname, 'document.ts'),  
  handler: 'createUser',  
  environment: {  
    TABLE_NAME: table.tableName,  
  },  
  ...sharedLambdaConfig,  
});  
table.grantWriteData(documentCreateUser);  
documentRoute.addMethod('POST', new cdk.aws_apigateway.LambdaIntegration(documentCreateUser));  
  
const documentListUsers = new cdk.aws_lambda_nodejs.NodejsFunction(this, 'DocumentListUsers', {  
  entry: join(__dirname, 'document.ts'),  
  handler: 'listUsers',  
  environment: {  
    TABLE_NAME: table.tableName,  
  },  
  ...sharedLambdaConfig,  
});  
table.grantReadData(documentListUsers);  
documentRoute.addMethod('GET', new cdk.aws_apigateway.LambdaIntegration(documentListUsers));  
 

These two lambda functions have basically the same configuration as the previous ones, except that they use the document.ts file as entry point, and are linked to a new API route.

### Use the DocumentClient SDK inside Lambda functions

Let's create a new file named document.ts in the same directory as the stack, and write the code of the lambda handlers inside. Using the DocumentClient SDK, it looks like this:  
 

import { DynamoDBClient } from '@aws-sdk/client-dynamodb';  
import { DynamoDBDocumentClient, PutCommand, QueryCommand } from '@aws-sdk/lib-dynamodb';  
  
const ddbClient = new DynamoDBClient({});  
const documentClient = DynamoDBDocumentClient.from(ddbClient);  
const tableName = process.env.TABLE_NAME ?? '';  
  
export const createUser = async (event: { body: string }) => {  
  const { username, email, age, adult } = JSON.parse(event.body) as {  
    username: string;  
    email: string;  
    age: number;  
    adult: boolean;  
  };  
  
  await documentClient.send(  
    new PutCommand({  
      TableName: tableName,  
      Item: {  
        PK: 'USER',  
        SK: username,  
        email,  
        age,  
        adult,  
      },  
    }),  
  );  
  
  return {  
    statusCode: 200,  
    body: JSON.stringify({  
      message: 'User created successfully',  
    }),  
  };  
};  
  
export const listUsers = async () => {  
  const { Items = [] } = await documentClient.send(  
    new QueryCommand({  
      TableName: tableName,  
      KeyConditionExpression: 'PK = :pk',  
      ExpressionAttributeValues: {  
        ':pk': 'USER',  
      },  
    }),  
  );  
  
  return {  
    statusCode: 200,  
    body: JSON.stringify({  
      users: Items.map(user => ({  
        username: user.SK,  
        email: user.email,  
        age: user.age,  
        adult: user.adult,  
      })),  
    }),  
  };  
};  
 

Let's break down the differences with the classic approach:

- First, we setup a documentClient that will send commands. It is built from the DynamoDBClient we already had (clearly showing how it is only a wrapper around the classic SDK).
- In the createUser Lambda handler, we can create a user using the PutCommand. This time, the code is easier to write and understand as the format is more natural.
- Same business in the listUsers Lambda handler. The ExpressionAttributeValues is cleaner and we don't have to use the .S .N .BOOL format when mapping the results.

With little effort, we already improved our developer experience! But there is still no type safety and autocompletion. All attributes are typed as any. It would also be cool if we could avoid writing technical attributes like PK and SK in our code. Let's see how we can do that using [dynamodb-toolbox](https://www.dynamodbtoolbox.com/)!

## Using dynamodb-toolbox to abstract DynamoDB technicalities

What is [dynamodb-toolbox](https://www.dynamodbtoolbox.com/)? In the documentation it is described as: "A set of tools that makes it easy to work with Amazon DynamoDB and the DocumentClient". Furthermore, it says, This is NOT an ORM!: it is a set of tools that help write commands and queries in a more natural way, but it is not an heavy abstraction layer like an ORM.

### Create the last two Lambda functions

Like before, let's create the last two Lambda functions in our CDK stack:  
 

const toolboxRoute = api.root.addResource('toolbox');  
  
const toolboxCreateUser = new cdk.aws_lambda_nodejs.NodejsFunction(this, 'ToolboxCreateUser', {  
  entry: join(__dirname, 'toolbox.ts'),  
  handler: 'createUser',  
  environment: {  
    TABLE_NAME: table.tableName,  
  },  
  ...sharedLambdaConfig,  
});  
table.grantWriteData(toolboxCreateUser);  
toolboxRoute.addMethod('POST', new cdk.aws_apigateway.LambdaIntegration(toolboxCreateUser));  
  
const toolboxListUsers = new cdk.aws_lambda_nodejs.NodejsFunction(this, 'ToolboxListUsers', {  
  entry: join(__dirname, 'toolbox.ts'),  
  handler: 'listUsers',  
  environment: {  
    TABLE_NAME: table.tableName,  
  },  
  ...sharedLambdaConfig,  
});  
table.grantReadData(toolboxListUsers);  
toolboxRoute.addMethod('GET', new cdk.aws_apigateway.LambdaIntegration(toolboxListUsers));  
 

### Use dynamodb-toolbox inside Lambda functions

[dynamodb-toolbox](https://www.dynamodbtoolbox.com/) works by creating entities. Entities are a way to describe a format for your items. You can define multiple entities inside a single table (it's called single-table-design), but here we only need to create a UserEntity. Then, you can use Entities to perform actions like creating, updating, deleting and querying items with a defined format inside the table.

Let's create a userEntity.ts file containing the definition of our UserEntity:  
 

import { DynamoDBClient } from '@aws-sdk/client-dynamodb';  
import { DynamoDBDocumentClient } from '@aws-sdk/lib-dynamodb';  
import { Entity, Table } from 'dynamodb-toolbox';  
  
const ddbClient = new DynamoDBClient({});  
const documentClient = DynamoDBDocumentClient.from(ddbClient);  
  
const table = new Table({  
  // WARNING: Only import this file in Lambda functions that have this environment variable  
  name: process.env.TABLE_NAME ?? '',  
  partitionKey: 'PK',  
  sortKey: 'SK',  
  DocumentClient: documentClient,  
});  
  
export const UserEntity = new Entity({  
  table,  
  name: 'USER',  
  attributes: {  
    username: { type: 'string', required: true },  
    email: { type: 'string', required: true },  
    age: { type: 'number', required: true },  
    adult: { type: 'boolean', required: true },  
    PK: { partitionKey: true, default: 'USER', hidden: true },  
    SK: { sortKey: true, default: ({ username }: { username: string }) => username, hidden: true },  
  },  
});  
 

As you can see at the beginning of the code, dynamodb-toolbox is built over the DocumentClient we previously covered. Here, the interesting part of the code is the definition of the attributes of the entity.

- username, email, age and adult are classical attributes, that have string, number and boolean types. We also specify that they are required, so that Typescript checks for us that we don't forget to set them when we create a user.
- PK is the partition key of the table. We know that it is a constant value, so we set it by default (this way there is no risk of making a typo inside Lambda handlers). Furthermore, we make it hidden so that it is not returned when we query the table. (we already know that queried items are users because we use the UserEntity)
- SK is the sort key of the table. We can set it by default dynamically, using the username attribute specified above. This way, when using the UserEntity to create a user, we don't have to set the SK attribute. It hides technical details from us, and makes our code cleaner. We also hide it so that returned items only contain the attributes we care about.

Now, let's use the UserEntity inside our Lambda handlers, by creating a new file named toolbox.ts in the same directory as the stack:  
 

import { UserEntity } from './userEntity';  
  
export const createUser = async (event: { body: string }) => {  
  const { username, email, age, adult } = JSON.parse(event.body) as {  
    username: string;  
    email: string;  
    age: number;  
    adult: boolean;  
  };  
  
  await UserEntity.put({  
    username,  
    email,  
    age,  
    adult,  
  });  
  
  return {  
    statusCode: 200,  
    body: JSON.stringify({  
      message: 'User created successfully',  
    }),  
  };  
};  
  
export const listUsers = async () => {  
  const { Items = [] } = await UserEntity.query('USER');  
  
  return {  
    statusCode: 200,  
    body: JSON.stringify({  
      users: Items.map(user => ({  
        username: user.username,  
        email: user.email,  
        age: user.age,  
        adult: user.adult,  
      })),  
    }),  
  };  
};  
 

The code has never been so clean! No more mentions to PK and SK, no more .S .N .BOOL format, no more ExpressionAttributeValues and KeyConditionExpression. The code is also strongly typed! If you forget to set an attribute when putting an item, Typescript will tell you. The result of the query is also typed, and you can use autocompletion to access the attributes of the returned items.

[![put-item-type](data:image/png;base64,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)](https://res.cloudinary.com/practicaldev/image/fetch/s--BWuk3hIw--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_800/https:/raw.githubusercontent.com/PChol22/kumo-articles/master/blog-posts/learn-serverless/ddb-toolbox/assets/put-item-type.png)

⬆️ If we forget to set adult, Typescript will tell us!

[![query-type](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABLYAAALwCAIAAAAF1WuJAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAAFiUAABYlAUlSJPAAABZQSURBVHhe7d3rchRV24BhI+GVjQiiKGIVeiLqsatnQiliEERBSNh+jX3rFyFMdrOf6yqqZz2ZpNIJP1J3Vk966+uvbr4HAAAA7733fo8AAABsvHYRv//hx3EGAABgA3337TfD0S4iAAAA+c8u4s2bXpcIAACwWW7dujUc7SICAADwHxIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIBIRAACASEQAAAAiEQEAAIhEBAAAIFtff3VzePj+hx+H482br9cAbKCXL18+fPiwgc1z6dKl99/3i2OADXXr1q3h+N233wxHiQjAa8+fP799+3YDm+fGjRvb29sNAGyY/Yno94UAAABEIgIAABCJCAAAQCQiAAAAkYgAAABEIgIAABA3vQDgtXfd9OLChQtXrlxpYPU9ePDg8ePHDfu46QXAJnNfRADe9K5EvHjx4ieffNLA6rt3795ff/3VsI9EBNhk7osIAADAASQiAAAAkYgAAABEIgIAABCJCAAAQCQiAAAAkYgAAABEIgIAABCJCAAAQCQiAAAAkYgAAABEIgIAABCJCAAAQCQiACyj58+f7+3t7e7uPn369OXLl70VAGZMIgLAEhmC8P79+z///PPt27d//fXXnZ2dO3fu/PTTT8P6zz//1IoAzJpEBICl8OLFi99++20IwkePHg3r3vqPvb29Bw8eDN34xx9/9CYAmAGJCACLNxTgEIePHz9ufoeXL18Oibizs2M7EYAZkYgAsGDPnj0bqu/tncN32d3dHd6/AQCmSiICwILdu3fv1atXDUfz9OlTV5wCMAsSEQAWaSi9ofcajuPEHwgAE0hEAFiYU24G3r9/vxUATIlEBICFefToUasTGQpzb2+vAQCmQSICwMLs7u62OqknT560AoBpkIgALJ0NuaPD8GU+f/684aS8HBGA6ZKIACyXhw8f/vLLL8+ePWteX0e/y8UEp49MANhPIgKwRIY+/P3334d22tnZWftKdPt7AJaQRARgWYx9OK43oRLPnDnT6hTef9+PcgCmyc8VAJbC/j4crX0lbm9vtzqFqXQmAPxLIgKweG/34WjtK/GDDz5odVLnzp1rBQDTIBEBWLB39eFovSvx/PnzrU7qwoULrQBgGiQiAIs0uQ9Ha1yJly5dOs3lph999JELTQGYLokIwMIcpQ9H61qJW1tbV69ebTims2fPXr58uQEApkQiArAYR+/D0bpW4rlz5z766KOG4xjacijMBgCYEokIwAIctw9H61qJly9fPu5fnbly5crp/9QNALxNIgIwb4f24YSX561lJW5tbX322Wcff/zxUXYFz549+/nnn59s4xEADiURAZirQ/twKKUvvvhiwhbZuu4lXrp06fr165P3BocyPPR9AOA0JCIA83OUPhxKadxV28BKHHcIB+Olp//73/+2t7eH78P58+evXr365ZdfXrlyxesP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JCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAEIkIAABAJCIAAACRiAAAAEQiAgAAkK2vv7o5PHz/w4/jDAAAwAb67ttvhqNdRAAAANIuIgAAANhFBAAA4G/vvfd/aurzuTX6mDsAAAAASUVORK5CYII=)](https://res.cloudinary.com/practicaldev/image/fetch/s--Nd6eylcw--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_800/https:/raw.githubusercontent.com/PChol22/kumo-articles/master/blog-posts/learn-serverless/ddb-toolbox/assets/query-type.png)

⬆️ The result of the query is typed

Finally, as you can see in the last screenshot, dynamodb-toolbox automatically generates attributes created and modified, that are the date of creation and last modification of the item. This is very useful to keep track of the history of your items!

## Stay tuned for dynamodb-toolbox v1 🚀

dynamodb-toolbox is currently in its 0.9.x version, many things can be improved like the typing of complex LIST and MAP attributes for example. Be reassured, the author is working on a v1 that will be released soon! It will use a simpler syntax and will be 100% type-safe, [check this article](https://dev.to/slsbytheodo/new-dynamodb-toolbox-v1-beta-features-and-breaking-changes-1ji5) to learn more about the beta version of this V1!

## Conclusion

There is no demo in this article as it would be quite trivial, but if you deploy the code, you can test the three API endpoints and see that they work the same way. The only difference is the code of the Lambda handlers, which is cleaner and more natural when using DocumentClient, and even better, dynamodb-toolbox.

dynamodb-toolbox has much more to offer, like the possibility to use indexes, perform updates, scans, get etc... I encourage you to read the [documentation](https://www.dynamodbtoolbox.com/) to learn more about it!

You can find the code of this article [here](https://github.com/PChol22/learn-serverless-ddb-toolbox).

### Let's connect!

I would really appreciate if you could react and share this article with your friends and colleagues. It will help me a lot to grow my audience. Also, don't forget to subscribe to be updated when the next article comes out!

I you want to stay in touch here is my [twitter account](https://twitter.com/PierreChollet22). I often post or re-post interesting stuff about AWS and serverless, feel free to follow me!

[Follow me on twitter 🚀](https://twitter.com/PierreChollet22)