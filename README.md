# Setup Auto Scaling for (Employee-API)

<img width="360" length="100" alt="Security" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/697fb29c-b84f-43bf-a48d-6c86d0ec41fa"> 

***

|   Author        |  Created on   |  Version   | Last updated by  | Last edited on |
| --------------- | --------------| -----------|----------------- | -------------- |
| Shreya Jaiswal |  21-02-2024  |  Version 1 | Shreya  | 21-02-2024    |
| Parasharam Desai | 21-02-2024 | Version 1 | Parasharam | 21-02-2024 |


***

## Table of Contents
+ [Introduction](#Introduction)
+ [Why use AWS Auto Scaling](#Why-use-AWS-Auto-Scaling)
+ [How AWS Auto Scaling Works](#How-AWS-Auto-Scaling-Works)
+ [Pre-requisites](#Pre-requisites)
+ [Steps To create Auto Scaling](#Steps-To-create-Auto-Scaling)
+ [Conclusion](#Conclusion)
+ [Contact Information](#Contact-Information)
+ [Resources and References](#Resources-and-References)
  
***

## Introduction

<img width="360" length="100" alt="Security" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/9061d024-a57d-47cf-8f73-5d3298a61441"> 

Amazon EC2 Auto Scaling allows you to manage the number of EC2 instances for your application automatically. You create groups of EC2 instances called Auto Scaling groups. You set minimum and maximum limits for the number of instances in each group. You can also specify how many instances you want at any given time. EC2 Auto Scaling adjusts the number of instances based on demand, launching or terminating them as needed.


***

## Why use AWS Auto Scaling

| Feature                                          | Description                                                                                                                |
|--------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **Monitoring the health of running instances**       | Automatically monitors instance health and replaces terminated or impaired instances to maintain desired capacity.         |
| **Custom health checks**                             | Define custom health checks to verify application response and automatically replace failing instances.                    |
| **Balancing capacity across Availability Zones**     | Distributes instances evenly across multiple Availability Zones for high availability and resiliency.                        |
| **Automated replacement of Spot Instances**          | Automatically requests replacement Spot capacity and proactively replaces instances at elevated interruption risk.         |
| **Load balancing**                                   | Utilizes Elastic Load Balancing for evenly distributing application traffic and automatically registering/deregistering instances. |
| **Scalability**                                      | Offers multiple scaling options to adjust capacity based on demand, maintaining availability and reducing costs.          |
| **Instance refresh**                                 | Updates instances in a rolling fashion with new AMIs or launch templates, supporting canary deployments for testing.       |
| **Lifecycle hooks**                                  | Defines custom actions triggered during instance launch or termination, useful for event-driven architectures.             |

***

## How AWS Auto Scaling Works

AWS autoscaling will scale the application based on the load of application. Instead of scaling manually AWS auto scaling will scale the application automatically when the incoming traffic is high it will scale up the application and when the traffic is low it will scale down the application.

<img width="460" length="100" alt="Security" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/9754a2aa-c29b-4969-8c20-f68bb20f032f"> 

First you should choose which service or an application you want to scale then select the optimisation way like cost and performance and then keep track how the scaling is working.
***
## Pre-requisites

  * Active AWS Account .

***

## Steps To create Auto Scaling

### Steps To create Launch Template  

  *  Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
  *  In the navigation pane, choose `Launch Templates`.

     <img width="760" length="100" alt="ASG" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/94584484-c221-4651-b20a-e0a22d7f8334"> 
 
  *  Click on the Create `launch template`.

      <img width="460" length="100" alt="ASG" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/77e3fa2a-a442-46fd-87d0-b4f639135c0e">

  * Type the Template name. eg `Dev-Employee-LT` and click on create launch template

      <img width="587" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/22263022-dfa2-431f-b57e-e3ab3b3a8d1a">


  * select the Amazon Machine Image (AMI) that has already been created,eg `Emloyee-API-AMI`

     <img width="656" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/3b67da77-4ee2-487e-b74c-e0c64aa75153">

  * Select the `Instance Type` and `Key Pair` and `subnet`.eg `t2-micro` `snaatak` `Backend-Pvt-Subnet` then click on create launch template.
  
     <img width="467" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/23ee3cea-4a70-4d00-b477-3af9010b42a1">
  
  * Now you can see the template is created. Now, scroll down and click on the `Auto Scaling Groups`.
    
     <img width="794" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/4910dde9-c2b8-40a3-88c9-ed109a18a195">


### Create An Auto Scaling Group Using a Launch Template

  * Click on the Create Auto Scaling group.

      <img width="660" length="100" alt="ASG" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/666c3d72-ef83-4a43-8177-ec7b0d9e5f20">

  * Type the Auto Scaling group name.eg `Dev-Employee-ASG` and template name eg `Dev-Employee-LT` and version eg `default(1)`.
  * Then Cilck `Next`.

     <img width="560" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/73cc9093-1e84-478b-bee5-bae1eb38f991">

   * Select the VPC and also select the Availability zone.eg `Dev-VPC` `Backend-Pvt-subnet`
   * Then Cilck `Next`.

     <img width="432" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/a41fdd4f-55a8-4afe-bb2e-e615843afee1">

  * Attach Load Balancer and Target Group and rest of the configurations will be default then cilck next.
   
     <img width="426" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/e019a14b-75a9-426b-8984-860a936fe9a9">

   * Configure the Group size and Scaling policies.
     
     Select as per your requirement:  
            * Desired: 1  
            * Minimum: 1  
            * Maximum: 2

      <img width="472" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/8e2cb560-2fe8-4ba4-86ff-097deff6bfa4">

  * Select the Target tracking scaling policy and rest of the configurations will be default then cilck next.

      <img width="660" length="100" alt="ASG" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/e7d48194-e62b-448a-a113-21593a0dc2f1">

  * This is optional step, if you want to add notificiation and tag, you can modify this otherewise, cilck next and skip this step, then click on `Create Auto Scaling group`.

     <img width="620" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/9d5b618c-42a9-447a-88ab-5c9c78ad8bde">

 * This is the ASG we created, as per our configuration, 2 instances created .  

     <img width="938" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/c92890ab-010c-463d-bbbe-33ad199d63f0">
  
  
***

## Conclusion

Amazon EC2 Auto Scaling manages your application's scalability by organizing instances into groups. It adjusts instance counts based on demand, offering features like health monitoring, custom checks, and load balancing. Simple steps help create Auto Scaling groups for dynamic scaling, optimizing performance and costs.

***

## Contact Information
| Name | Email address |
| ---- | ------------- |
| **Shreya Jaiswal** | shreya.jaiswal.snaatak@mygurukulam.co |
| **Parasharam Desai** | parasharam.desai.snaatak@mygurukulam.co |

***

## Resources and References

|  **Description** |   **Source** |
| ---------------- | ------------ |
| About Auto Scaling | [Link](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html) |
| Setup ASG | [Link](https://www.geeksforgeeks.org/create-and-configure-the-auto-scaling-group-in-ec2/) |
| Infra Diagram | [Link](https://github.com/CodeOps-Hub/Documentation/blob/main/Application_CI/Design/09-%20Cloud%20Infra%20Design/Cloud-Infra-Design-Dev.md) |


***
___________________________________________________________





# Setup Listener Rules for Load Balancer for (Frontend API)

<img width="300" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/6fd74997-5bda-4edc-bdc2-885df3b5e75f"> 

***

|   Author        |  Created on   |  Version   | Last updated by  | Last edited on |
| --------------- | --------------| -----------|----------------- | -------------- |
| Shreya Jaiswal |  21-02-2024  |  Version 1 | Shreya  | 21-02-2024    |
| Parasharam Desai | 21-02-2024 | Version 1 | Parasharam | 21-02-2024 |

***
## Table of Contents
+ [Introduction](#Introduction)
+ [Why use AWS Load Balancer](#Why-use-AWS-Load-Balancer)
+ [Listener Rules](#Listener-Rules)
+ [Importance of Listener Rules](#Importance-of-Listener-Rules)
+ [Pre-requisites](#Pre-requisites)
+ [Steps to setup Listener Rules for Load Balancer](#Steps-to-setup-Listener-Rules-for-Load-Balancer)
+ [Conclusion](#Conclusion)
+ [Contact Information](#Contact-Information)
+ [Resources and References](#Resources-and-References)
  
***
## Introduction

<img width="260" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/3a7244d7-a6dc-471b-bd80-bf6d500b02d0"> 

Load balancing in AWS refers to the process of distributing incoming network traffic across multiple servers or resources to ensure high availability and reliability of applications or services. The primary purpose of load balancing is to optimize resource utilization, maximize throughput, minimize response time, and avoid overloading any single resource.

***
## Why use AWS Load Balancer

| Benefit             | Description                                                                                                                                                                   |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **High Availability**   | Load balancers ensure application availability by distributing traffic across multiple servers. This minimizes downtime by routing requests to healthy instances.         |
| **Scalability**         | Load balancers enable horizontal scaling by dynamically adding or removing servers based on traffic demands. They distribute incoming requests across available resources. |
| **Fault Tolerance**     | Load balancers detect unhealthy instances and route traffic only to healthy ones, improving fault tolerance and reliability.                                                  |
| **Improved Performance** | Load balancers optimize request distribution based on factors like server health, geographic location, and network latency, improving overall application performance.   |
| **SSL Termination**     | Load balancers offload SSL/TLS decryption and encryption tasks, reducing computational overhead on backend servers and enhancing system performance.                         |

***
## Listener Rules

Listener rules in AWS load balancers determine how incoming traffic is routed to target groups based on request characteristics. Each rule, associated with a listener, prioritizes conditions like HTTP method, path, and source IP address, with lower priority numbers taking precedence. Actions include forwarding to target groups, redirecting, or returning fixed responses. Default rules handle unmatched requests by routing to a default target group or returning an error response.

***
## Importance of Listener Rules

Applications have various use cases in which we have to set up traffic routing based on various factors. Some applications have their setup as distributed microservices where the requests need to serve on the basis of the path to the different services. Sometimes, we may need to use a single load balancer for multiple applications and route the traffic based on the application URLs. These rules provide us a way to design our load balancing strategies according to our use cases and apply them without any complexities.

***
## Pre-requisites

 * Active Aws Account

***
## Steps to setup Listener Rules for Load Balancer
### Step 1: Configure a target group
  
  *  Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
  *  In the navigation pane, choose `Target Groups`.
  *  Choose Create target group.
 
   <img width="800" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/af210fdd-50b2-4f76-b6ab-911ca8ca7f8a">   
   
  *  Choose Create target group.
    
  <img width="800" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/0274d078-fed6-419b-9d51-a974fd613279">  
  
  * `Choose a target type` select `Instances` to specify targets by instance ID or IP addresses to specify targets by only IP address.
  * `Target group name` enter a name for the target group.eg `frontend-tg` and Port `3000`.
  * `VPC` select a virtual private cloud (VPC) with the targets that you want to include in your target group.eg `Dev-VPC`
  *  All configurtion default then Choose Next. 

 <img width="409" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/feeab858-d9c3-406a-a8b4-7708a51b3f9b">

 ***

### Step 2: Register targets

  * Select one or more instances, enter one or more eg `3000` ports, and then choose Include as pending below.
  * Then Choose Create target group.
    
 <img width="724" alt="image" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/01d96d2f-5085-4541-ba1c-8e9fd9892c0c">

***

### Step 3: Configure a load balancer and a listener
  
  *  Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
  *  In the navigation pane, choose Load Balancers.
  *  Choose `Create Load Balancer`.
 
  <img width="760" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/63694869-46f0-4609-894a-e6253b8433dd">   
  
  * Under Application Load Balancer, `Choose Create`.
    
  <img width="760" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/a27ebe0b-d905-42d8-a98e-8cbd63f80b0d"> 
  
  * `Load balancer name` enter a name for your load balancer. For example :- `DEV-ALB`.
  * Other  all configuration default .

 <img width="760" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/df209245-4109-471f-867e-cb3deb86f0af"> 

 * VPC select the VPC that you used for your EC2 instances.eg `DEV-VPC`
 * Mappings enable zones for your load balancer by selecting subnets from two or more Availability Zones.
 
 <img width="760" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/a9fc8a8a-d0c5-4718-9a68-a86805694888"> 

  * Security groups, select an existing security group, or create a new one. `with 80(HTTP) and 443(HTTPS)` `Frontend-lb-sg`
  * Listeners and routing, the default listener accepts HTTP traffic on port 80. You can keep the default protocol and port, or choose different ones.eg `Dev-employee-tg`.
  * Other  all configuration default .
     
<img width="760" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156057205/c3c02a66-e419-4c07-9c9f-c2aaeb9a0259"> 

  * Review your configuration and choose create load balancer. 

<img width="760" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/12c8aedb-027c-4897-9a78-ce20a36c47f1"> 

### Step 4: Test the load balancer

* Select the newly created load balancer.
* Choose Description and copy the DNS name of the internet facing or internal load balancer
* (for example, `Dev-ALB-1442510364.us-east-1.elb.amazonaws.com`).
  
<img width="760" length="100" alt="LB" src="https://github.com/CodeOps-Hub/Documentation/assets/156056413/0e988d1d-543b-4152-ad13-7a84e8962cb4">     

***

  * [**DNS**](http://dev-alb-1442510364.us-east-1.elb.amazonaws.com/api/v1/employee/health)
   
![image](https://github.com/CodeOps-Hub/Documentation/assets/156056709/94221ad0-1038-4cd0-a6fc-cf0f4ad0c2f6)


***
## Conclusion

This document offers a streamlined approach to implementing listener rules for load balancers within AWS. By understanding the significance of load balancing and the benefits provided by AWS Load Balancer, users can effectively optimize their application's performance, availability, and scalability. The step-by-step instructions provided in the document enable users to configure target groups, register targets, set up a load balancer and listener, and conduct thorough testing. This process ensures efficient traffic management, enhancing the overall reliability and responsiveness of applications hosted on AWS infrastructure.

***

## Contact Information
| Name | Email address |
| ---- | ------------- |
| **Shreya Jaiswal** | shreya.jaiswal.snaatak@mygurukulam.co |
| **Parasharam Desai** | parasharam.desai.snaatak@mygurukulam.co |

***

## Resources and References
|  **Description** |   **Source** |
| ---------------- | ------------ |
| About Listener Rules | [Link](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/listener-update-rules.html) |
| About Load Balancer | [Link](https://www.nginx.com/resources/glossary/load-balancing/) |
| Types of Load Balancer | [Link](https://kavishbaghel.com/utilising-listener-rules-for-load-balancing-using-aws-application-load-balancer-8e090e0ba469) |
| Follow this Infra Diagram | [Link](https://github.com/CodeOps-Hub/Documentation/blob/main/Application_CI/Design/09-%20Cloud%20Infra%20Design/Cloud-Infra-Design-Dev.md) | 


***



