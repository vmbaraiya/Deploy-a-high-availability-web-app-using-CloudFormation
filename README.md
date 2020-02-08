# Deploy-a-high-availability-web-app-using-CloudFormation


LoadBalancerDNS : http://webap-WebAp-YXXG2ROT3DPL-718651082.us-west-2.elb.amazonaws.com

---> Used Bastion Host to connect(SSH) to private Instances.

---> output exports of the CloudFormation server script is the  public URL of the LoadBalancer with http:// prefix.


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
 
 As I have used the Role for S3 so that EC2 instance can read the bucket, i have used the IAMInstanceProfile due to which we have to create the stack using below command ( need to use additional parameter ----capabilities CAPABILITY_IAM)
 
 
 $ aws cloudformation create-stack --stack-name webappserverstack \
    --template-body file://servers.yml \
    --parameters file://server-parameters.json --capabilities CAPABILITY_IAM

Log information for UserData scripts is located in this file: cloud-init-output.log under the folder: /var/log.


