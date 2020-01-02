### STAGE1 - CONFIGURE ANSIBLE ###
1) install ansible on ubuntu 16.04 
  # apt-get update
  # apt-add-repository ppa:ansible/ansible
  # apt-get update
  # apt-get install ansible
  # ansible --version

2) create user (gowtham)
  # adduser gowtham

3) we make gowtham user as a sudo user
  #  visudo
     gowtham ALL=(ALL) NOPASSWD: ALL
     :wq!

4) we have to connect to nodes  with out pem file.
  # vi /etc/ssh/sshd_config
    PasswordAuthentication yes
   :wq!
  # service ssh restart

### STAGE2 create IAM user and install pip###
1) Create IAM user(give - accessADMIN permission) 
2) Create AMI with ansible node
3) install pip on ansible master as root user

   #  apt-get install python-pip
   #  pip intall boto

4) Configure IAM user in ansible master as root user
vi .boto
   #  [Credentials]
   #  aws_access_key_id = foo
   #  aws_secret_access_key = bar
   :wq!

5) vi .boto credentials put it in user(gowtham) as well
   # $  [Credentials]
   # $  aws_access_key_id = foo
   # $  aws_secret_access_key = bar
   :wq!

### Stage3 Configure SSH ###
1) we should logging into any node using ssh-keygen
  
   $ ssh-keygen

2) copy key id into ansible nodes

   $ ssh-copy-id localhost

   $ ssh-copy-id <private ip of node>

### Start process for creating Dynamic inventory ###
1) write playbook for create ansible hosts in AWS as ansible user
   
   # $ create playbook by using ec2 module as below
   # $ check /Dynamic/createinstance.yml
     
2) Execute Playbook on localhost as ansible user

  $ vi myhost

  $ localhost

 :wq!

3) ssh-copy-id localhost

# ansible-playbook -i myhosts <playbookname.yml>

3) create ec2.py(Dynamic Inventory file) and ec2.ini( instructions file) as ansible user(gowtham)

4) change permissions of ec2.py and ec2.ini file with 755 and set as a global vars
   
  $ chmod 755 ec2.py ec2.ini
  
  $ export EC2_INI_PATH=/home/gowtham/dynamic/ec2.ini

  $ export ANSIBLE_HOSTS=/home/gowtham/dynamic/ec2.py

  $ ./ec2.py --list

# ansible tag_Name_AnsibleNode -i ec2.py -u gowtham -m ping

5) create playbook (check webserver.yml)
#  anible-playbook -i ec2.py -u gowtham  webserver.yml



