# Documentation on Web-Stack-Implementation-MERN-STACK-101-108
The MERN stack is a web development framework made up of the stack of MongoDB, Express, React.js, and Node.js. It is one of the several variants of the 
MEAN stack. When we use the MERN stack, you work with React to implement the presentation layer, 
Express and Node.js to make up the middle or application layer, and MongoDB to create the database layer.

## MERN-Stack-101 : EC2 instace and Virtual Ubuntu Server
AWS account was already created in previously done stack project. I have created another EC2 instance for MERN Stack Implentation.

### Created New EC2 instance and Setting up Ubuntu 
- First, created an ec2 instance named it as "Mern-instance" in a region "Stockholm" with instance type "t3.micro", AMI (Amazon Machine Image ) as "ubuntu", at first selected security group having inbound rules for (SSH,HTTP,HTTPS), later on added port 3000 and 5000  and all other required configuration was selected as default here.
 ![EC2 Instance](./images/t3_micro.png)
 ![EC2 Instance](./images/security_group1.png)
  ![EC2 Instance](./images/security_group2.png)
 ![EC2 Instance](./images/EC2.png)
- Latest version of ubuntu was selected which is "Ubuntu Server 22.04 LTS (HVM)". An AMI is a template that contains the software configuration (operating system, application server, and applications) required to launch your instance.
 ![Ubuntu AMI](./images/AMI_ubuntu.png)
- Private key was generated and named it as : "mern-stack-private" and downloaded ".pem" file.

### Connecting virtual server to EC2 instance
Used the same private key previously downloaded to connect to EC2 instace via ssh :
- Created security group configuration adding ssh and updated this configuration to my ec2 instance to access  TCP port 22.
- Changed the permission for "mern-stack-private.pem" file as :

  ```
  chmod 400 "mern-stack-private.pem"
  ```
- Connected to the instance as
  ```
  ssh -i "mern-stack-private.pem" ubuntu@ec2-16-171-38-244.us-east-2.compute.amazonaws.com
  ```
  This get changes as you stopped the ec2 instance and run again.
  ![Ubuntuip](./images/ubuntuip.png)

### Conclusion 
Linux Server in the cloud was created.

## MERN-Stack-102 : Backend configuration and  Installing the Node.js in the server
- Updated and Upgraded ubuntu EC2 instance :
  ```
    sudo apt update
    sudo apt upgrade
  ```
    ![UbuntuUpdate](./images/apt.png)
- Got the location of Node.js software from Ubuntu repositiorires :
  ```
    curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
  ```
    ![Nodejslocation](./images/locationubuntu.png)
    

- Installed Node.js on the server :
  ```
    sudo apt-get install -y nodejs
  ```
Note : The command above install both nodejs and npm. NPM is a package manager for Node, it is used to install Node modules and packages and to manage dependency conflicts.

- Verified node istallation :
  ```
    node -v 
    npm -v
  ```
    ![Nodeindtall](./images/nodeinstall.png)
### Appication Code SetUp
- Created a new directory for To-Do project :
  ```
    sudo mkdir
  ```

- Verified that the Todo directory is created :
  ```
    ls
  ```

- Changed current directory to the newly created one :
  ```   
    cd Todo
  ```

- Initialised the project :
  ```
    npm init
  ```
    ![Todo](./images/todo.png)
Note : A new file named package.json was created. This file will normally contain information about our application and the dependencies that it needs to run. 
    
### Conclusion

## MERN-Stack-103 : Installig ExpressJs and creating Routes 
Express helps to define routes of our application based on HTTP methods and URLs.
- Installed express using npm :
  ```
    npm install express
  ```

- Created a file index.js :
  ``` 
    touch index.js
  ```
    ![Express](./images/expressinstall.png)
- Installed the dotenv module :
  ```
    npm install dotenv
  ```

- Installed the index.js file and wrote the below given code :
  ```
    vim index.js
  ```
  ```
        const express = require('express');
        require('dotenv').config();
        
        const app = express();
        
        const port = process.env.PORT || 5000;
        
        app.use((req, res, next) => {
        res.header("Access-Control-Allow-Origin", "\*");
        res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
        next();
        });
        
        app.use((req, res, next) => {
        res.send('Welcome to Express');
        });
        
        app.listen(port, () => {
        console.log(`Server running on port ${port}`)
        });
  ```

- Started server to see if it works :
  ```
    node index.js
  ```
    ![Express](./images/dotenv.png)
- Accessed the server's public ip address and got output as :
    ![Server](./images/accessserver.png)

### Routes
There are three actio that our To-Do application needs to be able to do:
 1. Create a new task.
 2. Display list of all tasks.
 3. Delete a completed task.


