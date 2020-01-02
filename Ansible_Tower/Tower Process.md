# STAGE1 #
use below link for getting instance

# https://www.ansible.com/products/tower/trial

# STAGE2 #
1-Goto (LAUNCH ANSIBLE TOWER IN AMAZON EC2) and select which region tower instance you need

2-After creating instance connect with Centos user

3-copy the credentials and keep it with you
 # Username: admin
 # Password: NgfkNCHU7Pzp

4-create user and give visudo and ssh permission
 # sudo -i
 # adduser gowtham
 # passwd gowtham
 # visudo
   # gowtham ALL=(ALL) NOPASSWD: ALL
   :wq!
 # vi /etc/ssh/sshd_config
   # PasswordAuthentication yes
   # :wq!
 # service ssh restart

5-move to user and genrate key for password less authentication
 # su - gowtham

 $ ssh-keygen
 
 $ ssh-copy-id <node private ip>
 
# STAGE3 #
1-Take public ip and paste it in new webpage

2-give the credentials
 # Username: admin
 # Password: NgfkNCHU7Pzp
3-upload licence and login into tower webpage

4-Follow below process

 i)   create project 

 ii)  create credentials with your(UID and PASSWD)

 iii) create inventory(Give Groups and HOST)

 iv)  create template and execute it