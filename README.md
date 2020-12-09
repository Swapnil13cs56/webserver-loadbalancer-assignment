# Webservers with Loadbalancer Infra Setup 

This is a sample project which consists of 2 webservers and one loadbalancer using Vagrant, Ansible, HA Proxy and Virtualbox

## Pre-requisites

Following softwares/packages must be install in your system for running this project :-

Virtualbox (https://www.virtualbox.org/)  
Vagrant (https://www.vagrantup.com/)   

## Project Setup using Vagrant, Virtual Box and Ansible

This setup will spin up 4 virtual machines, namely web_server_1, web_server_2, loadbalancer and master.  
Since I am working on a windows machine, I thought of having an Ansible master machine, here the master machine is with name **master**.  

Follow the steps below to setup the required infrastructure  

- Step 1 Run **vagrant up**
- Step 2 Run **vagrant ssh master**
- Step 3 Run **ansible-playbook web-server-playbook.yml -i inventory**
- Step 4 Run **ansible-playbook loadbalancer-playbook.yml -i inventory --extra-vars 'sticky_session=false'**

## Result

To validate that the round robbin configuration in HA Proxy use curl  

Steps to follow  
- Step 1 Run the curl command on the master machine only which is **curl 192.168.56.103** here the ip is of loadbalancer or you can navigate to the same ip in browser as well
- Step 2 Run the above command repeatedly to check whether you are navigated to both the web servers or not (i.e 192.168.56.101 or 192.168.56.102)

## Bonus 

- Brief summary of what you liked about your solution
This assignment intergrates the devOps tools Ansible, Vagrant, Virtual Box, HA Proxy to create one of the Infrastructure solution

- Brief summary of what you disliked about your solution
Being on a windows system, I had to copy some of the files on the newly created master vm for ansible  

- Configurable Round Robin / Sticky Load Balancer
Yes, I have added both the configurations for loadbalancer. Based on the value of sticky_session passed, playbook will set haproxy.cfg file in loadbalance vm. 

- Return instance identifier of your webserver in addition to “Hello World”
Yes, I have included short javascript function which returns the URL of the page, which is the actual IP address in our case  


