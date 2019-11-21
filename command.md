# ping command
  ansible all -i myhosts -m ping
# playbook execution
  ansible-playbook -i myhosts .yml
# playbook syntax check
  ansible-playbook -i myhosts .yml --syntax-check
# Ad-hoc command
  ansible all -i myhost -b -m apt -a "name=tree"
# filter command
  ansible all -i myhosts -m setup -a "filter=*family*"
  ansible all -i myhosts -m setup -a "filter=*address*"
# java version check in nodes
  alternatives --config java
# listening port command
  netstat -ntulp
  jingar