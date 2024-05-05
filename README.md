# Task 2 - Infrastructure as code 

## Task description

You get a Node.js application from the Engineering team and your task is to deploy that application to the Cloud (AWS, Azure or GCP) in a
scalable fashion.
For this exercise, you may choose any non-trivial Node.js application that implements a REST API.
For example: https://github.com/digitalocean/sample-nodejs

## Task:

You can use any Cloud technology/service to create a scalable deployment: please explain why you chose that technology!
Your infrastructure should be defined as code
Briefly explain how to deploy and update your infrastructure (in your Readme)
Assume that your Node.js application is stateless, it does not need a database or similar to store data. But your application might
perform complex calculations or other longer operations.
Assume that your application will get a few million HTTP requests every day, but the exact load shape is unpredictable, there might be
usage spikes during peak hours
Try to optimize for overall cost and maintainability


## Solution

### Cloud Technology
I choose AWS as I intended to utilize Elastic Beanstalk to create an easily scalable environment, which is also cost cautious. The BeanStalk application will be controllable by a CloudFormation stack, using a template. 

### How to deploy and update the infrastructure
I created a CodePipeline and connected it to my github repository which contains the source node.js application and the CI/CD scripts. 
Upon any push event the pipeline is initiated and the Beanstalk application is refreshed. 
I also extracted the json script for the CodePipeline, and worked on transforming it to a working CloudFormation template, but it would need more testing and scripting to make it fully work. 
CodePipeline script: CodePipelineScript.json
Cloudformation template: CodePipelineScriptStack.yaml

### Application scaling
I configured an Auto Scaling group with Load balancing so if sudden load occurs we can dynamically allocate more instances. As for this example I only set the Max instances to 2 to avoid going above my free usage tier. 

### CloudFormation Stack 
I created a cloudformation template to manage the Elastic Beanstalk application. I used the new Git Sync function, so if we update the IaC in the repo it will trigger the template upate. 
Of course manual update is still possible. 
