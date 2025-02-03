# AWS-VPC-Traffic-Flow-And-Security

## Introduction
Think of the AWS Cloud as an entire country, and a VPC (Virtual Private Cloud) as your own private city within it. Just like a city has roads, buildings, and security checkpoints, your VPC has subnets, instances, and security controls that you can manage. You have full control over who enters, how traffic flows, and which areas remain private or public, ensuring a secure and customized environment tailored to your needs. 

## Use Case
This project demonstrates how to securely design and manage network infrastructure in AWS using a VPC (Virtual Private Cloud). By implementing subnets, security groups, route tables, internet gateways, and Network ACLs, it enables controlled access to cloud resources, ensuring secure data flow and minimized security risks. This setup is ideal for hosting web applications, deploying enterprise networks, or managing cloud-based workloads while maintaining scalability, security, and performance. 🚀

## Project Layout
<img width="854" alt="Screenshot 2025-02-02 at 6 50 46 PM" src="https://github.com/user-attachments/assets/4b91d246-4a91-4ca9-b887-af0c3df75038" />


## Project Solution

### <ins> Step 1: Create a VPC </ins>

Function: The internet gateway forwards the user's request to the VPC it's attached to.

VPC name: Avika VPC

IPv4 CIDR: 10.0.0.0/16
<img width="1262" alt="Screenshot 2025-02-02 at 6 28 00 PM" src="https://github.com/user-attachments/assets/5762af6c-6469-4f91-a853-26040c0c0150" />


### <ins> Step 2: Create a Subnet for this VPC </ins>

Function: The request enters your public subnet Public 1 and travels to your EC2 instance within the subnet.

Name: Public-01

After this, edit the subnet settings and enable auto-assign public IPV4 address (This is done so that any EC2 that is launched in this subnet will automatically get a public IP address, making it accessible without assigning a specific IP address manually.)
<img width="1273" alt="Screenshot 2025-02-02 at 6 28 12 PM" src="https://github.com/user-attachments/assets/f0d4be0c-8607-4236-a447-5d999e5aa1d6" />

### <ins> Step 3: Create an Internet Gateway: </ins>

Function: The request is sent from the user's browser through the internet and reaches your internet gateway.

This is used to connect the VPC to the internet. The EC2 instances with public IP addresses also become accessible to users, so any application you host on those instances become public too.

Name: My-gateway

After creating this, attach it to the VPC created above.
<img width="1512" alt="Screenshot 2025-02-02 at 3 44 02 PM" src="https://github.com/user-attachments/assets/fd19041e-2c96-4788-a11f-2e5783095619" />

### <ins> Step 4: Create a Route Table </ins>

Function: Your VPC has a route table for your public subnet (called NextWork route table), which directs traffic to your EC2 instance hosting the website. The user's request get put on the local route in the route table.

A route table decides where the data in this network goes. Every subnet needs to be linked to a route table.
Now the internet gatewat connected to the route table would know where to send the internet-bound traffic.

There would already be a route table created for the VPC, rename them.

Name: My-route-table
<img width="1512" alt="Screenshot 2025-02-02 at 6 15 24 PM" src="https://github.com/user-attachments/assets/402b7821-cb90-4423-ac3b-23419f6d290a" />

Also, add the subnet created above to this route table:

<img width="1505" alt="Screenshot 2025-02-02 at 6 16 50 PM" src="https://github.com/user-attachments/assets/8bb0908d-a174-43c1-94c9-e69ec51331ac" />

### <ins> Step 5: Create a Security Group </ins>

Function: The request reaches the security group NextWork Security Group attached to the EC2 instance. The security group has an inbound rule that allows HTTP traffic (Port 80) from anywhere (0.0.0.0/0), so the request can pass through.

Security Groups check what is the incoming and outoging traffic to the resource inside the VPC/subnet.

Security Group name: My-Security-Group

<img width="1512" alt="Screenshot 2025-02-02 at 6 23 39 PM" src="https://github.com/user-attachments/assets/2d8c0aad-068a-45d7-9513-18852f87d3e7" />

### <ins> Step 6: Create a Network ACL </ins>

Function: While en route to your EC2 instance, the request has to pass through the network ACL associated with your public subnet. The network ACL has an inbound rule (rule 100) that lets in traffic from anywhere (0.0.0.0/0), so your request is let through.

A Network ACL checks each data packet against a table of ACL rules before allowing them through. It gaurds the entire subnet.

While this applies to the entire subnet, a security group manages access to individual resources. 
This dual layer takes security to the next level as traffic must pass through multiple checks, which reduces the chances of unwanted access.(double security)

Name: my-ACL

To this, add all traffic inbound and outbound rule: (By default AWS denies all inbound and outbound traffic until manually changed.)

<img width="1271" alt="Screenshot 2025-02-02 at 6 33 21 PM" src="https://github.com/user-attachments/assets/7a448d98-6785-468b-8431-fdc0de83d8ec" />

Add the subnet created to the Network ACL (fulfilling the purpose of a Network ACL.)
<img width="1274" alt="Screenshot 2025-02-02 at 6 35 09 PM" src="https://github.com/user-attachments/assets/28df0cce-44f5-4cf4-ac2d-f4a08c5a927b" />


## This way the AWS VPC is structured, secured, and ready to host applications from potential cyber threats.

This process ensures a secure, scalable, and well-structured network environment within AWS by:

✅ Providing controlled access – Ensuring only authorized traffic reaches your resources through Security Groups and Network ACLs.

✅ Enabling internet connectivity – Allowing instances to communicate with the internet via Internet Gateways and Route Tables.

✅ Enhancing security – Implementing multiple layers of protection to reduce unauthorized access and potential threats.

✅ Optimizing network traffic flow – Ensuring efficient routing of data to enhance performance and reduce latency.

✅ Improving cloud infrastructure management – Allowing seamless scalability while maintaining strict access control and security compliance.









