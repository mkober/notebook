  

Clipped from: [https://conermurphy.com/blog/making-environment-variables-effortless-aws-cdk-stacks](https://conermurphy.com/blog/making-environment-variables-effortless-aws-cdk-stacks)

Learn to use environment variables in AWS CDK stacks to store sensitive data and user-specific settings and make them easily consumable inside any stack!

Environment variables are a vital part of any project, they allow us to easily store confidential information like API keys and secrets and user-specific configuration settings such as deployment regions and contact information, etc. So, when it comes to working with AWS CDK stacks, it’s important we use environment variables to ensure we don’t share this sensitive information as well as make it easier for others to set up and deploy the stack should we share it with them.

In this post, we’re going to look at how to configure environment variables to work with AWS CDK stacks and make them easy to consume and use anywhere in the stack with the help of a single configuration file.

The first thing we need to do in our CDK stack is create a new file (`` `.env` ``) in the root of our repository to contain our environment variables. Inside this file, we’re going to create two new environment variables.

```
1REGION = "eu-west-2";2LAMBDA_ENV = "test";
```

The first one we will use to control the AWS region we want to deploy to and the second one will be a variable we’ll pass through to a lambda function to demonstrate passing an environment variable through to a service configured in our CDK stack.

After this, we’re then going to add this `` `.env` `` file to our `` `.gitignore` `` file to make sure we don’t commit our environment variables by accident. Once our `` `.env` `` file is ignored in git, we’re going to install the `` `dotenv` `` package using `` `npm i dotenv` ``, this will allow us to read in our environment variables and use them in the project.

With that all sorted, let’s create the file that is going to let us access our environment variables from anywhere in the stack. To do this, create a new file in the `` `lib` `` directory called `` `config.ts` `` and add the below code.

./lib/config.ts

```
1import * as dotenv from "dotenv";2import path = require("path");3
4// 1. Configure dotenv to read from our `.env` file5dotenv.config({ path: path.resolve(__dirname, "../.env") });6
7// 2. Define a TS Type to type the returned envs from our function below.8export type ConfigProps = {9  REGION: string;10  LAMBDA_ENV: string;11};12
13// 3. Define a function to retrieve our env variables14export const getConfig = (): ConfigProps => ({15  REGION: process.env.REGION || "us-east-1",16  LAMBDA_ENV: process.env.LAMBDA_ENV || "",17});
```

ts

This file is pretty simple, we’re first importing `` `dotenv` `` and configuring it to read in our environment variables from the `` `.env` `` file we created. We’re then defining a TypeScript type that matches the environment variables we return from a `` `getConfig()` `` function.

This `` `getConfig()` `` function is where everything happens, we can call this function and get access to the values of our `` `.env` `` file and if for some reason they’re undefined, we’re able to define a fallback value as we have done with the `` `REGION` `` variable to fallback to `` `us-east-1` ``.

With our stack setup complete, let’s look at how we can consume our environment variables using the `` `getConfig()` `` function we just defined. First, let’s edit our stack entry file in our `` `bin` `` directory to control the region we’re going to deploy to as well as pass our config through to any stacks defined in the file. To do this, we’re going to use the code below.

./bin/*-stack.ts

```
1#!/usr/bin/env node2import "source-map-support/register";3import * as cdk from "aws-cdk-lib";4import { AwsEnvStack } from "../lib/aws-env-stack";5import { getConfig } from "../lib/config";6
7// 1. Retrieving our config and envs8const config = getConfig();9
10const app = new cdk.App();11
12new AwsEnvStack(app, "AwsEnvStack", {13  env: {14    // 2. Passing our REGION env to our stack to control the region it's deployed to15    region: config.REGION,16  },17  // 3. Passing our entire config to our stack as a prop for us to use.18  config,19});
```

ts

In this file, we retrieve our configuration using the `` `getConfig()` `` function. Then we use our `` `REGION` `` environment variable to define the region we’d like the stack to be deployed to. We also then pass our entire config as a prop to our stack so we can retrieve all of our environment variables from props instead of calling the `` `getConfig()` `` function again.

At this point, if you’re using TS you might get an error regarding the `` `config` `` being passed as a prop and it not being assignable to the type of `` `StackProps` `` so let’s sort that out in our stack definition file in our `` `lib` `` directory.

To fix the above-mentioned error we need to define a new type and use that to type the props being passed into the stack.

./lib/*-stack.ts

```
1import { Stack, StackProps } from "aws-cdk-lib";2import { Construct } from "constructs";3import { NodejsFunction } from "aws-cdk-lib/aws-lambda-nodejs";4import { ConfigProps } from "./config";5
6// 1. New type for the props adding in our configuration7type AwsEnvStackProps = StackProps & {8  config: Readonly<ConfigProps>;9};10
11export class AwsEnvStack extends Stack {12  // 2. Consuming our type for `props` and making props mandatory13  constructor(scope: Construct, id: string, props: AwsEnvStackProps) {14    super(scope, id, props);15
16    // 3. Retrieving our config with our environment variables from the props17    const { config } = props;18  }19}
```

ts

So, with the above code, we define a new type that extends `` `StackProps` `` to also include our `` `config` `` object with the type we created earlier as the return type of the `` `getConfig()` `` function. We then use this new type to type the props being passed into the stack before pulling our `` `config` `` object out of the props.

At this point, we can now use our environment variables from our `` `config` `` object inside our CDK stack as well as with the services defined inside our stack. To demonstrate this let’s create an example lambda function to log out our environment variable from earlier. To do this create a new file at `` `./resources/test-lambda.ts` `` and add in the below code.

./resources/test-lambda.ts

```
1export const handler = () => {2  console.log(process.env.LAMBDA_ENV);3};
```

ts

Let’s now define our new lambda function inside our CDK stack definition file in our `` `lib` `` directory by adding the below code under where we destructured our `` `config` `` object earlier.

./lib/*-stack.ts

```
1// ...rest of the stack definition2const { config } = props;3
4// Lambda definition5new NodejsFunction(this, "TestLambda", {6  entry: "./resources/test-lambda.ts",7  handler: "handler",8  environment: {9    LAMBDA_ENV: config.LAMBDA_ENV,10  },11});
```

ts

The important part to note in this definition is the environment object where you can see we’re passing in the `` `LAMBDA_ENV` `` from our `` `config` `` object. This is then consumed in the lambda function using `` `process.env.LAMBDA_ENV` `` which is then logged out. And, with this lambda function defined and configured, we’ve finished writing our CDK stack so let’s move on to deploying and testing it!

To deploy our CDK stack run `` `cdk deploy` `` in your terminal and accept any prompts given to you by the console.

**NOTE:** You may need to install the `` `esbuild` `` package with `` `npm i esbuild` `` as we’re using the `` `NodejsFunction` `` construct which requires this package to deploy.

Once your stack has finished deploying you can check if the region environment variable worked as planned by reviewing the deployment logs in your terminal. Towards the top of the logs, you should see mentioned the region you’re deploying to, this should align with the `` `REGION` `` environment variable you configured earlier.

To test if the `` `LAMBDA_ENV` `` environment variable and all of the setup we did worked as planned, we can invoke the lambda by using the CLI with the command below (make sure to switch out `` `LAMBDA_NAME` `` with the name of your deployed lambda which you can get from your AWS dashboard or CLI).

```
1aws lambda invoke --function-name  LAMBDA_NAME   --invocation-type Event -
```

Once your lambda has been invoked, check the log outputs for it in CloudWatch by using the AWS dashboard and you should see the value of the `` `LAMBDA_ENV` `` from earlier logged out. If this is the case, congrats, everything is working as planned and you have environment variables configured in your AWS CDK stack!

During this post, we’ve looked at why environment variables are important to a project as well as how you can use them inside an AWS CDK stack by using a single configuration file and passing the config to our stacks as props.

If you’d like to see the full example code for this blog post [you can view the GitHub repository here](https://github.com/conermurphy/cdk-tutorials/tree/main/stack-envs). And, if you’d like to see the [accompanying video for this blog post, you can watch it on YouTube here.](https://youtu.be/yJ74jWIH3rc)

I hope you found this post helpful.

Thank you for reading

Coner

**👥 1370**