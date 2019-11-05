# Importing-OVA-to-AWS
(Based on this link: https://meetrix.io/blog/aws/ec2/import-export.html)
This is a guide how to import an OVA file to AWS so that it can be an instance.

# Create a trust-policy.json file
Basically have the trust-policy.json file in the local machine.

# Create a role-policy.json file
Basically have the role-policy.json file in the local machine.

# Create a containers.json file
Basically have the containers.json file in the local machine.


# Run appropriate AWS commands to create rules
aws iam create-role --role-name vmimport --assume-role-policy-document file://trust-policy.json
aws iam put-role-policy --role-name vmimport --policy-name vmimport --policy-document file://role-policy.json

# Run appropriate AWS command to import image to EC2
aws ec2 import-image --description "MyVM" --license-type BYOL --disk-containers file://containers.json

# To check the status of converting from image to EC2
aws ec2 describe-import-image-tasks --import-task-ids import-ami-<id>
  
# Side Notes
The import-ami-<id> can be found from a JSON based returns importing images.


