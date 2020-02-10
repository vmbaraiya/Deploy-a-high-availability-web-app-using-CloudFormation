# Deploy-a-high-availability-web-app-using-CloudFormation

This project helps to practice skills with Infrastructure as a code using cloudformation.

### Getting Started

* AWS CloudFormation is a service that helps you model and set up your Amazon Web Services resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and AWS CloudFormation takes care of provisioning and configuring those resources for you. You don't need to individually create and configure AWS resources and figure out what's dependent on what; AWS CloudFormation handles all of that. The following scenarios demonstrate how AWS CloudFormation can help.

     •	CloudFormation is a declarative language, not an imperative language.

     •	CloudFormation handles resource dependencies, so that you don’t have to specify which resource to start up before another. There are cases where you can specify that a resource depends on another resource, but ideally, you’ll let CloudFormation take care of dependencies.

* [diferrence between Declarative and Imperative Languages](https://en.wikipedia.org/wiki/Imperative_programming)

*With the right template, you can deploy at once all the AWS resources you need for an application. In this section, you'll examine a template that declares the resources for deploying high availability web app*

* [VPC Template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-vpc.html)
* [Auto Scaling template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/quickref-autoscaling.html)
* [EC2 template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_EC2.html)
* [Load Balancer](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-elasticloadbalancingv2-loadbalancer.html)
* [Parameters](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html)
* [DependsOnAtrribute](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-dependson.html)

### Diagrams

 * Diagrams are a very important starting point for planning your cloud infrastructure. DevOps engineers start with a visual representation of the required cloud infrastructure before they turn it into code. 

![Diagram for deployment](https://github.com/vmbaraiya/Deploy-a-high-availability-web-app-using-CloudFormation/blob/master/CloudFormation-Project.png)

## Prerequisite
 * AWS Account
 * Visual Studio
 * [AWS CLI ](https://aws.amazon.com/cli/)
 * python
 * YAML
 * JSON
 * Shell Script
 
 Configure AWS CLI with user key for programmatic access:
 ```shell
aws configure 
AWS Access Key ID [None]: 
AWS Secret Access Key [None]: 
Default region name [None]: 
Default output format [None]:
```

```shell
aws --version
aws-cli/1.17.9 Python/3.6.0 Windows/10 botocore/1.14.9
```

### AWS Cludformation create Stack and Update Stack

 - Create Stack
```shell
 $ aws cloudformation create-stack --stack-name <stackname> \
    --template-body file://<stackyamlfile> \
    --parameters file://<parameterjsonfile> 
```
 - Update Stack
```shell
 $ aws cloudformation update-stack --stack-name <stackname> \
    --template-body file://<stackyamlfile> \
    --parameters file://<parameterjsonfile>
```

 * Log information for UserData scripts is located in this file: cloud-init-output.log under the folder: /var/log.

### Stack Files 

    * create.sh ==> Script to create new cloudformation stack. Requires following arguments in order:
        ./create.sh <stack name> <YAML template file name> <JSON Parameter file name>
  
    * update.sh ==> Script to update the cloudformation stack. requires following arguments in order:
       ./update.sh <stack name> <YAML template file name> <JSON Parameter file name>

   1. Create Network Stack using Network Stack files
   
       1a. network.parameters.json ==> parameter file for cloudformation  stack to create network components.
       
       1b. network.yml  ==>  cloudformation yaml file to create the network stack ( VPC, subnets, NAT gateway, Internet Gateway)
       
     
   2. create Server Stack using Server stack files
   
      2a. server-parameters.json ==> parameter file tfor cloudformation stack to create infrastructure.
      
      2b. servers.yml ==> cloudformation yaml file to create infrastructure stack ( Security group, Instances, Load Balancer, Bastion host, Auto Scale, Listener, listener rule, targets)
      
      **To Use IAMInstance profile with EC2 Instance for accessing AWS Resource like S3:**
      use below create stack command with --capabilities argument
      
      ```shell
      $ aws cloudformation create-stack --stack-name webappserverstack \
      --template-body file://servers.yml \
      --parameters file://server-parameters.json --capabilities CAPABILITY_IAM
      ```
      
**Command line**
```shell
aws s3 cp <file name> <link to S3 bucket>  
```
 This line above copies a file from your local machine to the S3 bucket
 
### CloudFormation retention policy
   •	You'll want your data to persist even if your stack of resources is updated or deleted.
   •	 [Retention policy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-deletionpolicy.html): keeps a service even if the entire stack of infrastructure is marked for removal. In CloudFormation, the syntax is DeletionPolicy: retain. This is very useful to assign to your data storage (database, file storage), to make sure that your data is saved even when the stack is updated or deleted.

 
 ### Reference Documents for more details:
 * [Architecture](https://aws.amazon.com/architecture)
 * [Time-Series-Processing-architecture](https://d1.awsstatic.com/architecture-diagrams/ArchitectureDiagrams/aws-reference-architecture-time-series-processing.pdf?did=wp_card&trk=wp_card)
 * [AWS-Refarch-wordpress](https://github.com/aws-samples/aws-refarch-wordpress?did=wp_card&trk=wp_card)
 * [Subnet](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-subnet.html)
 * [NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html#nat-gateway-creating)
 * [Internet Gateway](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-internetgateway.html)
 * [Outputs](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/outputs-section-structure.html)
 * [Substitutes](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-sub.html)
 * [Join Functions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-join.html)
 * [Launch Configuration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-as-launchconfig.html)
 * [Target Groups](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-elasticloadbalancingv2-targetgroup.html)
 * [Health Checks for Target Groups](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/target-group-health-checks.html)
