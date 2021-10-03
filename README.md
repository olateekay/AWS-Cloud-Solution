# AWS-Cloud-Solution
AWS Cloud solution for 2 company websites using reverse proxy technology


The requirement is to have an infrastructure that can serve 2 or more different websites at the lowest possible
infrastructure and cloud cost, and still able to satisfy HA and security requirements.


Options

1. Create multiple AWS accounts with dedicated VPC per environment - More secured but a lot of monthly AWS bills

2. Create a single AWS account and multiple VPCs for each environment - (What does an environment mean?) - lowered cost
3. Create a single AWS account, Single VPC, and multiple subnets for each environment. - lowered cost


Requirements
1. Developers should simply deploy their code and each environment will always have the deployed version of the application (CI/CD)
2. The customers/Users should not know the backend implementation of each website. Meaning it shouldn't be obvious that the same load balancer is serving multiple website requests.

Example sites....
www.darey.io
www.cowboyshop.com
www.sicklecell.org

Resources

1. VPC
2. Subnets
3. Internet Gateway
4. Route Tables [public and private subnets]
5. Route table association
6. Attach Internet Gateway to the VPC
7. Elastic IPs 
8. Nat Gateway
9. Security Groups

    -- External Public Facing Application Load Balancer - Accessible to everyone on the internet, or limited to the country it serves over the internet. on port 80/443
    
    -- Nginx Servers  - Accessible ONLY to the ALB on port 80/443, and bastion from port 22

    -- Internal Non-Public Facing Application Load Balancer - Accessbile only from Nginx load balancer

    -- Bastion Servers - Accessible only to company engineers on port 22

    -- Webservers - Accessbile only from Nginx servers and Bastion servers on port 80 and 22 respectively

    -- Data Layer - Accessible only from the webservers on relevant ports.
        RDS/Aurora-MySQL - 3306
        EFS - 2049

10. AMI [Nginx, Apache, Bastion]

11. Launch Templates

12. Auto Scaling Group

13. ALB (Internal and External)

14. Aurora/MySQL (RDS)

15. EFS (NFS)

16. ACM 
