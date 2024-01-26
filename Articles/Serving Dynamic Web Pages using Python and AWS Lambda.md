  

Clipped from: [https://adamnovotny.com/blog/serving-dynamic-web-pages-using-python-and-aws-lambda.html](https://adamnovotny.com/blog/serving-dynamic-web-pages-using-python-and-aws-lambda.html)

Published: 2020-07-25 .[](https://medium.com/@adamnovotnycom/serving-dynamic-web-pages-using-python-and-aws-lambda-864ff810fc5c/)

While AWS Lambda functions are typically used to build API endpoints, at their core Lambda functions can return almost anything. This includes returning html markup with dynamic content.

[![AWS Lambda + Python + Jinja](https://adamnovotny.com/theme/images/1*9bPdHLV7ghV1RuNYOGkTvA.png.png)](https://adamnovotny.com/theme/images/1*9bPdHLV7ghV1RuNYOGkTvA.png.png)

I will not go into details describing how to deploy AWS Lambda functions. Please see the official [documentation](https://docs.aws.amazon.com/lambda/latest/dg/lambda-python.html). I will however describe how to return dynamic html content instead of a typical [JSON](https://en.wikipedia.org/wiki/JSON).

#### Step 0 — Optional

If you prefer to develop and test lambda functions locally (as I do), you can use Docker to simulate the AWS lambda function environment. A sample Dockerfile I use is below.

FROM amazonlinux:latest
RUN mkdir -p /mnt/app
ADD . /mnt/app
WORKDIR /mnt/app
RUN yum update -y
RUN yum install gcc -y
RUN yum install gcc-c++ -y
RUN yum install findutils -y
RUN yum install zip -y
RUN amazon-linux-extras install python3=3.6.2
RUN pip3 install --upgrade pip
RUN pip3 install -r requirements.txt -t aws_layer/python

The requirements.txt includes just one package for simplicity. It is the common [templating for Python called Jinja2](https://jinja.palletsprojects.com/en/2.11.x/)

Jinja2==2.11.1

You can test your Lambda function by simple calling it with sample parameters:

import lambda_function
event = {
    "queryStringParameters": {
        "param1": "value1"
    },
    "path": "/api",
    "requestContext": {
         "param2": "value2"
    }
}
res = lambda_function.lambda_handler(event=event, context={})
assert 200 == int(res["statusCode"])

#### Step 1 — Write html template

In this step, we write the html template the Lambda function will return. A good default is the new [Bootstrap 5](https://v5.getbootstrap.com/docs/5.0/getting-started/introduction/) CSS framework where the recommended starting markup looks something like this:

[![Sample HTML page](https://adamnovotny.com/theme/images/1*b3ZXkCsw8BwLt2Fx_eu6PQ.png.png)](https://adamnovotny.com/theme/images/1*b3ZXkCsw8BwLt2Fx_eu6PQ.png.png)

Saving this file in folder “templates” and naming it index.html, we are ready to write the Lambda function.

#### Step 2 — Write Lambda function to serve your html page

In the example below, the lambda function expects URL parameters and parses those. So when parsing a custom URL, the format would look something like this: Example.com/?my_name=somename. See step 10 in [this tutorial](https://adamnovotny.com/blog/serverless-web-apps-with-firebase-and-aws-lambda.html) to add custom URLs to your API Gateway-triggered Lambda functions.

import os
import sys
from jinja2 import Environment, FileSystemLoader

def lambda_handler(event, context):
    env = Environment(loader=FileSystemLoader(os.path.join(os.path.dirname(__file__), "templates"), encoding="utf8"))
    my_name = False
    if event["queryStringParameters"] and "my_name" in event["queryStringParameters"]:
        my_name_query = event["queryStringParameters"]["my_name"]
    template = env.get_template("index.html")
    html = template.render(
        my_name=my_name_query
    )
    return response(html)

def response(myhtml):
    return {
        "statusCode": 200,
        "body": myhtml,
        "headers": {
            "Content-Type": "text/html",
        }
    }

- jinja2 loads your previously created index.html using class “FileSystemLoader” and we store it as variable “env”

- variable “my_name” is parsed from the URL query parameters as explained above and stored as the Python variable my_name_query

- the jinja2 render function then passes my_name_query to the template and returns the html page

Also published on [adamnovotny.com](https://adamnovotny.com/)