### Create a Resource group
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/317374ed-bda8-41f1-8817-5f4b97aee7a8)
### Create a Virtual network
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/2541a105-9ac9-4c0f-90ff-e937fd37485a)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/feb4b5df-bc61-4c50-a571-1826cb2be693)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/5a3e33cd-3a3b-4b99-8c10-4f89a7e86275)

>[!INFO]
>The bastion host is used to access the virtual machine that does not have the public IP address.

![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/129290d4-6d6d-49c2-9c85-91d02dd1f53a)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/1e31b4ac-f760-4694-b86a-f1e6f2c8e573)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/cac18f45-9ae2-4f51-aa5b-e68112d650e3)

### Create a Virtual machine
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/5b83327d-bcfa-4343-b85b-e5bb8f10a693)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/76d9bc27-a94c-4a03-94d9-ac888112d5c5)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/5050bd74-8234-4baa-858d-bb591728b873)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/514e4648-b246-46a3-9275-7a1b969f546c)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/6587bbae-779e-4e1c-b791-2a6103fd163d)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/5124249b-be49-4ab2-82a3-02e2c001cebe)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/ab88535a-fcf7-4786-8f8d-8fd3a495f4ac)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/4aa74d82-3680-4d5c-8264-926f191648ce)
>[!INFO]
>The custom data is like the user data in the AWS which will allow the script to run when the VM is initiated. And user data in Azure will store the script to the lifetime of the VM.

![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/169383ae-1800-4ae2-a8c2-d7d429bcbb6a)

### Bastion Server
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/2d9cd11a-48f3-4e4a-82d4-0498cf6cf906)
>[!INFO]
>Enter the virtual machine and connect  to the bastion with SSH private key. Select the .pem file that we downloaded.

![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/cfd5e38c-137b-4d8e-a759-a3b6aef4d088)
>[!note]
>run the following commands
>`sudo su -` change to root user
>`apt-get update`
>`apt-get install nginx -y`

>[!note]
>Now change directory `cd /var/www/html` 
Now add an index.html file for the nginx server to serve you. And then restart the inginx server `systemctl restart nginx`
In order to check if the nginx server is working you need to curl and see the content, nginx server port 80. `curl localhost 80`

### Configure the Firewall
>[!INFO]
>
>The aim of this configuration is to give users an ip address which they can use to access the webpage

![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/f38af308-2984-4f03-b300-988795c956db)
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/e4cf633a-4472-43ea-84c6-3b4731f00c43)

>[!CHECK] 
>
>This is the location to get the IP address of the firewall and paste it in the destination tab.
>![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/b759b772-bf6e-4e44-932a-c94cd20d85f0)
>This is the location to get the private IP address of the Virtual machine. This IP should be entered in Translated address.
![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/0cb3f16c-48d2-432b-8e33-a8d7387350d0)


>[!INFO] 
>With all the above information create the rule and eventually create the firewall policy.

![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/2cdf5ff3-a9c0-47bd-beed-8b8c5b80f76e)

>[!QUESTION]  
><u>Difference between DNAT rule and NAT gateway:</u>
>In Azure, when you refer to a "DNAT rule," you are likely talking about configuring a Network Security Group (NSG) rule that involves Destination Network Address Translation (DNAT). DNAT in this context is a way to translate the destination IP address of incoming network traffic.
Here's how it works: 
1.**Destination Network Address Translation (DNAT) in Azure NSG:**
In an Azure NSG, you can create an inbound security rule that includes DNAT. This rule allows you to forward traffic from a specific public IP address and port to a specific private IP address and port inside your Azure Virtual Network.
This is often used when you want to expose a service running on a specific virtual machine within your Azure network to the public internet. The DNAT rule helps in translating the destination IP address and port.
   2. **Network Address Translation (NAT) in Azure:** Azure provides a service called Azure NAT Gateway, which performs source network address translation for outbound traffic. It allows virtual machines within a private subnet to access the internet without having public IP addresses. This is different from DNAT, as NAT Gateway is primarily concerned with translating the source IP address of outgoing traffic.                                                           In summary, DNAT in an Azure NSG is a mechanism to allow inbound traffic to be forwarded to specific resources inside your Azure network, while Azure NAT Gateway is a service that allows outbound traffic from private resources to access the internet using a shared public IP address. They serve different purposes but both involve some form of network address translation. 

![image](https://github.com/karthi770/Jira_GitHub_intergration_Python/assets/102706119/f38af308-2984-4f03-b300-988795c956db)
>[!IMPORTANT] 
>If you could see there is an option to attach the firewall policy, we need to add the created firewall policy .


Hi
bye


