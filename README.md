# Employee
Employee Directory Web-App Using AWS Cloud

When highlighting your employee directory web app project on your resume, it's important to use specific keywords and phrases that showcase your skills and the technologies you used. Here's a step-wise procedure with main keywords you can use in different sections of your resume:

1. **Summary/Objective:**
    - AWS Cloud Project
    - Web Application Development
    - Flask Python Framework
    - Security and VPC Implementation
    - AWS EC2, Lambda, and S3
2. **Skills:**
    - AWS Services (EC2, Lambda, S3)
    - VPC (Virtual Private Cloud)
    - Flask Python Framework
    - Security Implementation
    - Firewall Configuration
    - Subnetting
    - Web Application Development
    - Database Integration (if applicable)
3. **Project Section:**
    - **Project Title:** Employee Directory Web App
    - **Description:** Developed a secure and scalable employee directory web application using AWS services and Flask Python framework. Key components included:
        - AWS EC2 for hosting the web application
        - AWS Lambda for serverless functions
        - AWS S3 for storage and file handling
        - VPC and Security Groups for network isolation
        - Firewall configuration for enhanced security
        - Subnetting for fine-grained control
4. **Project Details:**
    - **AWS Services:**
        - Utilized AWS EC2 instances for hosting the web app, ensuring high availability and scalability.
        - Leveraged AWS Lambda for serverless functions, optimizing resource utilization.
        - Employed AWS S3 for storing and managing employee data and assets securely.
    - **Security and Networking:**
        - Configured a Virtual Private Cloud (VPC) to isolate the project resources, enhancing security.
        - Implemented security groups and network ACLs to control inbound and outbound traffic.
        - Utilized firewall rules to restrict unauthorized access and enhance data protection.
        - Employed subnetting to segment the network for improved control and resource organization.
    - **Web Development:**
        - Developed the web application using the Flask Python framework, providing a user-friendly interface for employee data management.
        - Integrated a database system (mention the database technology) to store and retrieve employee information (if applicable).
5. **Achievements/Results:**
    - Successfully delivered a secure, scalable, and user-friendly employee directory web app.
    - Implemented robust security measures, resulting in zero security breaches.
    - Achieved efficient resource utilization through AWS Lambda, reducing operational costs.
    - Improved data organization and network control with subnetting and VPC implementation.
    - Received positive feedback from users regarding the application's performance and user interface.
6. **Technologies Used:**
    - AWS (EC2, Lambda, S3)
    - Flask Python Framework
    - Virtual Private Cloud (VPC)
    - Security Groups and Network ACLs
    - Firewall Configuration
    - Subnetting
    - Database Integration (mention the specific database technology, if applicable)

By using these keywords and phrases in your resume, you can effectively communicate your experience and skills related to your employee directory web app project using AWS and Flask Python.

Let me show you the EXECUTION Step-Wise 

Task 1: Launching an EC2 instance that uses a role

In this task, you will launch an EC2 instance that hosts the employee directory application.

1. If needed, log in to the AWS Management Console as your *Admin* user.
2. In the **Services** search bar, search for **EC2**, and open the service by choosing **EC2**.
3. In the navigation pane, under **Instances** choose **Instances**.
4. Choose **Launch instances**.
5. For **Name** use `employee-directory-app`.
6. Under **Application and OS Images (Amazon Machine Image)**, choose the default **Amazon Linux 2023**.
7. Under **Instance type**, select **t2.micro**.
8. Under **Key pair (login)**, choose **Create a new key pair**.
9. For **Key pair name**, paste `app-key-pair`. Choose **Create key pair**. The required **.pem** file should automatically download for you.
10. Under **Network settings** and **Edit**: Keep the default VPC selection, which should have *(default)* after the network name
    - **Subnet**: Choose the first subnet in the dropdown list
    - **Auto-assign Public IP**: *Enable*
11. Under **Firewall (security groups)** choose **Create security group** use `app-sg` for the **Security group name** and **Description**.
12. Under **Inbound security groups rules** choose **Remove** above the **ssh** rule.
13. Choose **Add security group rule**. For **Type** choose **HTTP**. Under **Source type** choose **Anywhere**.
14. Expand **Advanced details** and under **IAM instance profile** choose **S3DynamoDBFullAccessRole**.
15. In the **User data** box, paste the following code:
    
    ```bash
    #!/bin/bash -exwget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/FlaskApp.zipunzip FlaskApp.zipcd FlaskApp/yum -y install python3-pippip install -r requirements.txtyum -y install stressexport PHOTOS_BUCKET=${SUB_PHOTOS_BUCKET}export AWS_DEFAULT_REGION=<INSERT REGION HERE>export DYNAMO_MODE=onFLASK_APP=application.py /usr/local/bin/flask run --host=0.0.0.0 --port=80
    ```
    
    !https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/images/clipboard.svg
    
16. In the pasted code, change the following line to match your Region (your Region is listed at the top right, next to your user name):
    
    ```bash
    export AWS_DEFAULT_REGION=<INSERT REGION HERE>
    ```
    
    !https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/images/clipboard.svg
    
    Example:
    
    The following example uses the US West (Oregon) Region, or *us-west-2*.
    
    ```bash
    export AWS_DEFAULT_REGION=us-west-2
    ```
    
    !https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/images/clipboard.svg
    
    **Note:** In a later lab, you will modify this user data script again to use your Amazon Simple Storage Service (Amazon S3) bucket. For now, keep **`${SUB_PHOTOS_BUCKET}`** in the script.
    
17. Choose **Launch instance**.
18. Choose **View all instances**.
    
    The instance should now be listed under **Instances**.
    
19. Wait for the **Instance state** to change to *Running* and the **Status check** to change to *2/2 checks passed*.
    
    **Note**: Often, the status checks update, but the console user interface (UI) might not update to reflect the most recent information. You can minimize waiting by refreshing the page after a few minutes.
    

## Task 2. Viewing the application

In this task, you will view the application that’s running on the instance in a web browser window.

1. Select the instance by selecting its check box.
    
    Instance information should load on the tabs in the pane.
    
2. On the **Details** tab, copy the **Public IPv4 address**.
    
    **Note**: Make sure that you only copy the address instead of choosing the **open address** link.
    
3. In a new browser window, paste the IP address that you copied. *Make sure to remove the ‘S’ after HTTP so you are using only HTTP instead*.
    
    You should see an **Employee Directory** placeholder. Right now, you won’t be able to interact with it yet because the application isn’t connected to a database.
    
    Congratulations! You have successfully created an EC2 instance, which hosts the employee directory application.
    
    After you finish exploring the instance, you will stop and terminate your instance so that you don’t incur future costs.
    

## Task 3. Cleaning up

In this task, you will terminate the EC2 instance that you launched.

1. Go back to the AWS Management Console.
    
    The *employee-directory-app* instance should still be selected.
    
2. At the top of the console pane, choose **Instance state**, choose **Stop instance**, and choose **Stop**.
    
    The status in the **Instance state** column will eventually go into the *Stopped* state.
    
    Next, you will terminate the instance.
    
3. Make sure that check box next to the instance **Name** is selected.
4. Choose **Instance state**, choose **Terminate instance**, and choose **Terminate**.


