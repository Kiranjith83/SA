SDLC (22% on exam.  system development and lifecycle)

# CI/CD 
- Continuous integration 
    - Compiling code
- Continuous deployment
    - Process of code publish

# CodeCommit

# CodeBuild

# CodePipeline 

# Testing. 
- Why we need testing?
    - It makes sure that:
        - Meet the requirements defined
        - Ensure the code performs in an acceptable period of time.
        - ensure its usable.
        - ensure it responds correctly to all kinds of inputs.
        - Achieves the desired results
- Types of Software testing. 
    - Installation testing. 
    - Compatability testing.
    - Smoke and sanity testing. 
    - Regression testing.
    - Acceptance testing
    - Alpha/Beta testing
    - Functional vs non-functional testing
    - Continuous testing
    - Destructive testing.
    - Software performance testing. 
    - Usability/accessibility testing.
    - AB Testing
    - Sec testing
- Automated test execution can be part of CI/CD process.
    - Unit testing is the way to perform testing in automated way.


# CodeArtifact
- Secure, scalable, and cost-effective artifact management

# Deployment strategies
## Single target deployment.
    - Deploy to a single target.
## All at once deployment. 
    - Perform deployment to multiple targets 
    - Conducted by orchestration tooling or using any kind of automation.
    - Shares negative of single target as no ability to test, can have deployment outages and les than ideal for rollback.
    - Used for non critical deployment. 
## Minimum in-Service deployment.
    - Keeping min number of instance in service at a time. 
    - Deployment happens in multi stages.
    - No downtime and can do automated testing.
## Rolling deployment. 
    - Deployment happens in stages and only proceed further if the initial deployment is successful.
    - Orchestration and health check is required for this method.
    = Rollback can be performed.
## Blue Green deployment.
    - Blue: Current environment 
    - Green: Perform upgrade by creating the green environment. 
    - A method for swapping the DNS entry with new env is required.
    - Entire method can be automated. 
    - No split of traffic, and the cut over is binary (Either green or blue)
## Canary deployment
    - Both the Blue and Green are kept active and a percentage of traffic is routed in steps to the new env.
    - It can be achieved using Route53 - Weighted round robin traffic policy

# CloudFormation

# Beanstalk

# AWS Config
- AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources. 
- Constantly monitors and looks for changes to the AWS Configuration. 
- It can capture the state of configuration at a given point of time.

# AWS Managed Services

# Lambda
- 1 million free req per month. 

# Step Functions.

# OpsWorks

# CloudWatch
- Data points < 60 Sec are available for 3 hours.
- Data points ~= 60 sec (1 min) available for 15 days. 
- Data points ~= 300 sec (5 mins) available for 63 days. 
- Data points ~= 3600 sec (1 hour) available for 445 days (15 months).

## CW Events
- AWS Resources can generate an event when there is a change in its environment.
    - Eg: EC2 instance state changed from Pending to Starting. 
## CW Rules
- Matches the incoming events and routes them to a target for an action.
## CW Targets
- Target process the events. It receives the event in the json format. 
    - Ex: Lambda, Kinesis, SNS and many more.