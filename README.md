# Ansible OpenVPN

First off all you have to configurate the network. for that add the line
>ONBOOT=yes\
>NAME=enp0s3
>
in the file
> /etc/sysconfig/network-scripts/ifcfg-enp0s3

and after just restart interface with
> ifdown enp0s3 && ifup enp0s3

if the name of your interface is already enp0s3 

After, create hosts file : 
>[hosts]\
>IP OF HOST (192.168.X.X)\
>[hosts:vars]\
>ansible_user=root\
>ansible_ssh_pass='password'\
>ansible_become_pass='password'\
>[hosts:vars]\
>ansible_ssh_common_args='-o StrictHostKeyChecking=no'\

just change "password", "IP OF HOST" and "root" if your user is not root.

the last file to fill out is in roles/openvpn/defaults/main.yml, and configure your variables

>client_name: client_name\
>password_private_key : password_of_the_private_key


Now you can run the receipt 
> ansible-playbook -i hosts main.yml

# Create USER
if you just want create a user you can run : ansible-playbook -i hosts main.yml -t create_client

# Reinstallation
Be carefull if you want re create user certificate, delete old certificate