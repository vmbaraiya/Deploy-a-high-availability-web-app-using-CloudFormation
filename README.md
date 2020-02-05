# Deploy-a-high-availability-web-app-using-CloudFormation

CloudFormation-Project.png 
    -- This is task diagram for creating cloudformation code.

create.sh ==> Script to create new cloudformation stack. Requires following arguments in order:
./create.sh <stack name> <YAML template file name> <JSON Parameter file name>
  
 update.sh ==> Script to update the cloudformation stack. requires following arguments in order:
 ./update.sh <stack name> <YAML template file name> <JSON Parameter file name>
