## Deploy-a-high-availability-web-app-using-CloudFormation

This project helps to practice skills with Infrastructure as a code using cloudformation.

### Getting Started

* AWS CloudFormation is a service that helps you model and set up your Amazon Web Services resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and AWS CloudFormation takes care of provisioning and configuring those resources for you. You don't need to individually create and configure AWS resources and figure out what's dependent on what; AWS CloudFormation handles all of that. The following scenarios demonstrate how AWS CloudFormation can help.

•	CloudFormation is a declarative language, not an imperative language.
•	CloudFormation handles resource dependencies, so that you don’t have to specify which resource to start up before another. There are cases where you can specify that a resource depends on another resource, but ideally, you’ll let CloudFormation take care of dependencies.

*[diferrence between Declarative and Imperative Languages](https://en.wikipedia.org/wiki/Imperative_programming)

*With the right template, you can deploy at once all the AWS resources you need for an application. In this section, you'll examine a template that declares the resources for deploying high availability web app*

* [VPC Template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-vpc.html)
* [Auto Scaling template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/quickref-autoscaling.html)
* [EC2 template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_EC2.html)
* [Load Balancer](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-elasticloadbalancingv2-loadbalancer.html)


![Diagram for deployment](https://github.com/vmbaraiya/blueocean/blob/master/output.png)

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

```shell
 $ aws cloudformation create-stack --stack-name *stackname* \
    --template-body file://stackyamlfile \
    --parameters file://parameterjsonfile --capabilities CAPABILITY_IAM
```

* Log information for UserData scripts is located in this file: cloud-init-output.log under the folder: /var/log.


### Files 
CloudFormation-Project.png 
    -- This is task diagram for creating cloudformation code.

create.sh ==> Script to create new cloudformation stack. Requires following arguments in order:
./create.sh <stack name> <YAML template file name> <JSON Parameter file name>
  
 update.sh ==> Script to update the cloudformation stack. requires following arguments in order:
 ./update.sh <stack name> <YAML template file name> <JSON Parameter file name>


 network.parameters.json ==> parameter file for cloudformation  stack to create network components.
 
 network.yml  ==>  cloudformation yaml file to create the network stack ( VPC, subnets, NAT gateway, Internet Gateway)
 
 server-parameters.json ==> parameter file tfor cloudformation stack to create infrastructure.
 
 servers.yml ==> cloudformation yaml file to create infrastructure stack ( Security group, Instances, Load Balancer, Bastion host, Auto Scale, Listener, listener rule, targets)
 
 
 ### Reference Documents for more details:
 
