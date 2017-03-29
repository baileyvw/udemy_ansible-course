Ansible basics training
visudo
root ALL=(ALL) ALL
%admin  ALL=(ALL) ALL
ansible ALL=(ALL) NOPASSWD: ALL
================================
create ansible user account and ssh key for the ansible user with no password 
do a ssh-keygen on each server
ssh-keygen 

now copy the ssh key the server
copy ssh key from your master serverto any of servers you want to run ansible

scp id_rsa.pub ansible@yservername.com:/home/ansible/.ssh/authorized_keys

or

ssh-copy-id ansible@servername (no password)

Also make sure you are using git and github or bitbucket to version control your files.
