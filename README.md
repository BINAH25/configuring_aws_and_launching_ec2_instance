# configuring_aws_and_launching_ec2_instance

1. **Installing aws cli:**
   ```bash
    sudo apt install awscli
    
![alt text](image.png)

2. **verifying the installation:**
   ```bash
    aws --version
    
![alt text](image-1.png)


3. **configuring the aws cli:**
   ```bash
    aws configure
    
![alt text](image-2.png)


4. **creating a named profile:**
   ```bash
    aws configure --profile myprofile
    
![alt text](image-3.png)

5. **finding available Amazon Machine Image (AMI):**
   ```bash
    aws ec2 describe-images --owners amazon --query "Images[*].[ImageId,Name]" --output table
    
![alt text](image-4.png)

6. **creating a key pair:**
   ```bash
    aws ec2 create-key-pair --key-name dev --query "KeyMaterial" --output text --profile myprofile > dev.pem


7. **launching an ec2 instance:**
   ```bash
    aws ec2 run-instances --image-id ami-0866a3c8686eaeeba --count 1 --instance-type t2.micro --key-name dev --profile myprofile

    
![alt text](image-5.png)
![alt text](image-6.png)

8. **verifying that the instance is running:**
   ```bash 
    aws ec2 describe-instances --profile myprofile --query "Reservations[*].Instances[*].[InstanceId,State.Name]" --output table
    
![alt text](image-7.png)

9. **obtaining the public address of the instance:**
   ```bash 
    aws ec2 describe-instances --profile myprofile --query "Reservations[*].Instances[*].[PublicIpAddress]" --output table
    
![alt text](image-8.png)

1. **ssh into the instance:**
   ```bash 
    ssh -i dev.pem ubuntu@ec2-44-203-156-189.compute-1.amazonaws.com
    
![alt text](image-9.png)


2. **terminating the instance:**
   ```bash 
    aws ec2 terminate-instances --instance-ids i-05d391dff39e320a8 --profile myprofile
    
![alt text](image-10.png)


3. **verifying that the instance is terminated to avoid charges:**
   ```bash 
    aws ec2 describe-instances --profile myprofile --query "Reservations[*].Instances[*].[InstanceId,State.Name]" --output table
    
![alt text](image-11.png)
