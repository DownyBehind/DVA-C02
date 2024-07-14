# AWS Elastic Beamstalk

## OverView

Developer problems on AWS

- Managing infrastructure
- Deploying Code
- Configuring all the databases, load balancers, etc
- Scaling concerns

- Most web apps have the same architecture (ALB + ASG)
- All the develoers want is for their code to run!
- Possibly, consistently across different applications and environments

- Elastic Beanstalk is a developer centric view of deploying an application on AWS
- It uses all the component's we've seen before: EC2, ASG, ELB, RDS,...
- Managed service
: Automatically handles capacity provisioning, load balancing, scaling, application health monitoring, instance configuration,...
: Just the application code is the responsibility of the developer

- We still have full control over the configuration
- Beanstalk is free but you pay for the underlying instances

Components

Application: Collection of Elastic Beanstalk components (environments, versions, configurations, ...)

Application Version: an iteration of your application code 

Environment 
- Collection of AWS resources running an application version (only one application version at a time)
- Tier: Web Server Environment Tier & Worker Environment Tier 
- You can create multiple environments (dev, test, prod, ...)

## Beanstalk First Environment 

## Beamstalk Second Environment

## Beanstalk Deployment mode

Beanstalk Deployment Options for Updates

- All at once (deploy all in one go) - fastest, but instances aren't availiable to serve traffic for a bit (downtime)

- Rolling: Update a few instances at a time (bucket), and then move onto the next bucket once the first bucket is healthy

- Rolling with additional batches: like rolling, but spins up new instances to move the batch (so that the old application is still available)

- Immutable: spins up new instances in a new ASG, deploys version to these instances, and then swaps all the instances when everything is healthy

- Blue Green: create a new environment and switch over when ready

- Traffic Splitting: canary testing - send a small % of traffic to new deployment

