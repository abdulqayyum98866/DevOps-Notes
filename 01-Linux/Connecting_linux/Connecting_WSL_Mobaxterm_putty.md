# 1 - Install Windows Subsystem for Linux (WSL)
## References
- [Windows Subsystem for Linux (WSL)] (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-linux-inst-ssh.html)
## To connect to your instance using an SSH client
- Open a terminal window on your computer.
- Locate the .pem key
- cd to the location of .pem key
- (Linux instances) Set the permissions of your private key so that only you can read it.
  ```bash
  #chmod 400 key-pair-name.pem
  ```
- (Public DNS) To use the public DNS name, enter the following command.
   ```bash
   ssh -i /path/key-pair-name.pem instance-user-name@2001:db8::1234:5678:1.2.3.4
   ```
- Enter `yes` 
- Now SSH done!
# 2 - Connect to your Linux instance using PuTTY
## References
- [Linux instance using PuTTY)] https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-linux-inst-from-windows.html

# 3 - Connect to EC2 Using MobaXterm

##MobaXterm is an SSH client used on Windows to connect to Linux EC2 instances.

**Steps**

- Open MobaXterm

- Click Session → SSH

- Enter the Public IP / DNS of the EC2 instance

**Set Username:**

ubuntu (Ubuntu)

ec2-user (Amazon Linux)

- Enable Use private key

- Select your .pem key file

- Click OK / Connect

- You will be logged into the ```EC2 instance``` successfully.
  
