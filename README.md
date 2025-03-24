# AWS-VPC-Networking
This repository provides an AWS VPC architecture setup designed for a highly available and secure cloud infrastructure. It includes public and private subnets, an Internet Gateway (IGW), NAT Gateways, and a Virtual Private Gateway (VPG) for hybrid cloud connectivity. The architecture spans multiple Availability Zones (AZs) to ensure fault tolerance and scalability.
It serves as a reference for deploying scalable, secure, and cost-efficient AWS network architectures, suitable for hosting applications, databases, and hybrid cloud environments.
### Key Features:
 - Multi-AZ Deployment for high availability
 - Public & Private Subnets for better security control
 - NAT Gateway for outbound internet access from private subnets
 - VPN Connectivity to on-premises corporate networks
 - Modular & Scalable infrastructure design
# Creating VPC in AWS with 2 public and private subnet.
## Concept Used
  - **Virtual Private Cloud (VPC)**
    - A Virtual Private Cloud is a logically isolated section of the AWS cloud where you can launch resources in a virtual network you define. A VPC allows you to control 
      your network settings such as IP address ranges, subnets, route tables, and gateways.
  - **Subnets**
    - Subnets are subdivisions of a VPC that allow you to group resources by IP range within an Availability Zone. Subnets can be public (accessible from the internet) or 
      private (isolated from the internet).

  - **Internet Gateway (IGW)**
    - An Internet Gateway is a VPC component that allows resources in public subnets to access the internet. It serves as a target for internet-bound traffic in the route 
      table of a public subnet.

  - **Virtual Private Gateway (VPG)**
    - A Virtual Private Gateway is a VPN concentrator on the AWS side of a VPN connection. It allows private subnets to securely communicate with other private networks, 
      such as on-premises environments or other VPCs.
  - **Route Table**
    - A Route Table contains a set of rules, called routes, that determine where network traffic is directed.
  - **Availability Zone (AZ)**
    - An Availability Zone is a distinct location within an AWS Region that is engineered to be isolated from failures in other zones, providing high availability.
      
## Architectural Overview of VPC
  - **VPC Configuration**
     - **CIDR Block**: `10.0.0.0/16`
  - **Subnet Configuration**  
     - **Availability Zone :1** :
       - Public Subnet 1: `10.0.0.0/20`
       - Private Subnet 1: `10.0.128.0/20`
     - **Availability Zone :2** :
       - Public Subnet 2: `10.0.16.0/20`
       - Private Subnet 2: `10.0.192.0/20`
  - **Gateways**
    - **IGW**: Connects Public Subnet 1 and Public Subnet 2 to the internet.
    - **VPG**: Connects Private Subnet 1 and Private Subnet 2.
  ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/whole%20resource%20map.png)
 ## Step By Step Way to Create this Architecture

  **Step 1:-** **Create a VPC**.
   -  Go to AWS Console and navigate to **VPC Dashboard**.
     ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/vpc%20dashboard.png)

   -  Click **Create VPC**
        -  Name as `MyVPC`
        -  Choose **IPv4 CIDR block**: `10.0.0.0/16`.
          ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/create%20vpc.png)
        -  Leave all other options as default.
   -  Click **Create VPC**.
     ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/created%20vpc.png)
  
  **Step 2:-** **Creating Subnets**
   -  **Availability Zone :1**
      -  Navigate to VPC Dashboard.
      -  Click on **Create Subnet :**
          - Name: `PublicSubnet-1`.
          - Choose your VPC : `MyVPC`.
          - Choose a Availability Zone :`us-east-1a`
          - IPv4 CIDR Block: `10.0.0.0/20`.
            ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/pus1.png)
      - Click **Create Subnet**.
        ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/pus1a.png)
      - Repeat the step to create Private Subnet in the same availability zone.
          - Name: `PrivateSubnet-1`.
          - Choose your VPC : `MyVPC`.
          - Choose a Availability Zone :`us-east-1a`
          - IPv4 CIDR Block: `10.0.128.0/20`.
          - Click **Create Subnet**.
            ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/ps1.png)
        - This will create one Public Subnet and one Private subnet in **us-east-1a** zone.
      -  **Availability Zone :2**
           - Navigateto VPC Dashboard.
           - Click on **Create Subnet :**
               - Name: `PublicSubnet-2`.
               - Choose your VPC : `MyVPC`.
               - Choose a Availability Zone :`us-east-1b`
               - IPv4 CIDR Block: `10.0.16.0/20`.
               - Click **Create Subnet**.
                 ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/pus2.png)
            - Repeat the step to create Private Subnet in the same availability zone.
               - Name: `PrivateSubnet-2`.
               - Choose your VPC : `MyVPC`.
               - Choose a Availability Zone :`us-east-1b`
               - IPv4 CIDR Block: `10.0.192.0/20`.
               - Click **Create Subnet**.
                 ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/ps2.png)
            - This will create one Public Subnet and one Private subnet in **us-east-1b** zone.
           [](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/all%20subnet.png)   
 **Step 3:-** **Create an Internet Gateway (IGW)**
   - Navigate to Internet Gateways in the **VPC Dashboard**.
   - Click Create **Internet Gateway**:
      - Name: `MyIGW`.
        ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/igw%20creating.png)
   - Click Create.
     ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/igw2.png)
   - Attach your **VPC** to the **Internet Gateway**  that is `MyIGW` to `MyVPC`.
      - Select the **Internet gateway** `MyIGW`.
      - Then click on **Actions** and then select `Attach to VPC`.
       ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/attaching%20igw.png) 
      - Choose `MyVPC`.
        ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/attaching%20igw2.png)
      - Then click on **Attach**.
        ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/attached%20igw.png)
        
**Step 4:-** **Creating a Virtual Private Gateway (VPG)**
   - Navigate to **Virtual Private Gateways** in the **VPC Dashboard**.
   - Click **Create Virtual Private Gateway**:
       - Name: `MyVPG`.
       ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/vpg.png)
       - Leave the **Autonomous System Number (ASN)** as default.
   - Click Create.
     ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/vpg2.png)
   - Attach your **Virtual Private Gateway** to your **VPC** that is  `MyVPG` to `MyVPC`:
       - Select the  **Virtual Private Gateway** `MyVPG`.
       - Click on **Actions** and then select `Attach to VPC`.
         ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/attaching%20vpg1.png)
       - Choose `MyVPC`.
         ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/attaching%20vpg2.png)
       - Then click on **Attach to VPC**.
         ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/attached%20vpg.png)
         
**Step 5:-** **Configuring  Route Tables**
  - **Public Route Table**:
    - Navigate to *Route Tables* in the *VPC Dashboard*.
    - Create a route table for public subnets:
      - Click **Create Route Table**.
      - Name: `PublicRouteTable`.
      - Select VPC: `MyVPC`.
        ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/publicroute%20table.png)
    - Add a route for internet traffic:
      - Select the route table`PublicRouteTable`.
      - Then click on **Routes tab** and then on **Edit Routes**.
        ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/editing%20public%20table.png)
      - Click on **Add Route**.
      - Choose **Destination**: `0.0.0.0/0`
      - Select Target as your **Internet Gateway** `MyIGW`.
        ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/editi%20public%20route.png) 
    - Associate public subnets with the route table:
      - Click on **Subnet Associations** and then on **Edit Subnet Associations**.
        ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/editing%20subnet%20ass.png)
      - Select your Public Subnets: `PublicSubnet-1` & `PublicSubnet-2`.
        ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/editing%20subnet%20ass%20choosing%20public%20subnet%20.png)
        ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/public%20route%20table%20final.png)
 - **Private Route Table**:
   - Create a route table for private subnets:
     - Click **Create Route Table**.
     - Name: `PrivateRouteTable`.
     - Select your VPC :`MyVPC`.
       ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/private%20route%20table.png)
   - Enable route propagation for the VPG:
     - Select the route table `PrivateRouteTable`.
     - Click on **Route Propagation tab** and then on **Edit Route Propagation**.
       ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/editing%20route%20propagation.png)
     - Select your VPG : `MyVPG`.
       ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/enable%20route%20propgation.png)
   - Associate private subnets with the route table:
     - Click on **Subnet Associations** and then on **Edit Subnet Associations**.
       ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/editing%20subnet%20assocition%20in%20private.png)
     - Select your Private Subnets: `PrivateSubnet-1` & `PrivateSubnet-2`.
       ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/private%20subnet%20associotion.png)
       ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/final%20private%20route%20table.png)

**Step 6:-** **Launching  EC2 Instances**
  - **Public Subnets**
     - Launch an EC2 instance in `PublicSubnet-1`:
       - Select an AMI (e.g., Amazon Linux 2).
       - Configure networking to use `PublicSubnet-1`.
       - Assign a public IP address.
     - Repeat the process for `PublicSubnet-2`.
       ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/public%20instaNCES1.png)
   - **Private Subnets**
      - Launch an EC2 instance in `PrivateSubnet-1`:
        - Step 1: Navigate to the *EC2 Dashboard* and click *Launch Instance*.
        - Step 2: Choose an AMI (e.g., Amazon Linux 2 or Ubuntu).
        - Step 3: Choose an instance type (e.g., t2.micro).
        - Step 4: Configure instance details:
          - Network: Select your VPC `MyVPC`.
          - Select Subnet: `PrivateSubnet-1`.
          - Auto-assign Public IP: *Disable*.
          - Leave other options as default or customize as needed.
        - Step 5: Add storage (default is fine).
        - Step 6: Add tags (optional, e.g., `Key: Name`, `Value: PrivateInstance-1`).
        - Step 7: Configure security group:
          - Create or select a security group that allows SSH access from a specific IP or CIDR block.
        - Step 8: Review and launch:
          - Select an existing key pair or create a new one for SSH access.
            - Click **Launch**.
     - Repeat the process for `PrivateSubnet-2`, selecting the corresponding subnet.
     ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/all%20instancres.png)

## Configuring the Security Group for SSH Access
  - **Step 1:-** **Navigate to the Security Groups Section**
      - Log in to the *AWS Management Console*.
      - Open the *VPC Dashboard* or *EC2 Dashboard*.
      - On the left-hand navigation menu, click Security Groups under Network & Security.
  - **Step 2:-** **Create a New Security Group**
      - Click the *Create security group button*.
      - Configure the following settings:
         - Name tag: Enter a name for the security group (e.g., Private-SSH-Access).
         - Description: Provide a description (e.g., Allows SSH access from specific IP).
         - VPC: Select the VPC (`MyVPC`) where your instance resides.
  - **Step 3:-** **Configure Inbound Rules**
      - Under the Inbound rules section, click *Add rule*.
      - Define the SSH rule as follows:
         - Type: `SSH`.
         - Protocol: `TCP` (auto-filled when SSH is selected).
         - Port Range: `22`.
         - Source: Select one of the following:
            - My IP: Automatically fills in your current public IP address.
            - Custom: Enter a specific IP or CIDR block. For example:
             - Single IP: `203.0.113.25/32` (allows only this IP).
             - CIDR Block: `192.168.1.0/24` (allows all IPs in this range).
         - **Anywhere-IPv4** (Not recommended for private instances): `0.0.0.0/0` (allows SSH access from any IPv4 address).
       - Click **Save rules**.
         ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/creating%20sg.png)
   - **Step 4:-** **(Optional) Configure Outbound Rules**
      - By default, all outbound traffic is allowed. If you need to restrict outbound traffic:
        - Click the *Outbound rules section*.
        - Add or modify rules as needed (e.g., limit outbound traffic to specific IPs or services).
   - **Step 5:-**  **Attach the Security Group to Your Instance**
     - Navigate to the *EC2 Dashboard*.
     - Select the instance where you want to apply the security group.
     - Click *Actions* → *Security* → *Change security groups*.
     - Select the `Private-SSH-Access` security group you just created.
     - Click **Save**.
## Testing and Verification
 - Verify public instances have internet access via their public IPs.
   ![](https://github.com/ravikantmaurya00/AWS-VPC-Networking/blob/main/ScreenShot/apache%202.png)
 - Ensure private instances communicate only via the VPG.
 - Use SSH or ping to test connectivity between instances.




