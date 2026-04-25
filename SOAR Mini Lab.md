# SOAR Lab

**Submited By**: Nizamudheen KN  
**Date**: 24-04-2026  
**Subject**: SOAR Automation  

---

So Inorder to set up the lab I use AWS because my system was having low specs. In AWS i created 3 Ubuntu 24.04 Server Instance. The instance called `zoooi` running wazuh manager in docker. The instance called `n8n` is running my n8n in docker. The instance called `balake server` running as an endpont with the wazuh agent installed. This is my setup and it is easy to set it up in AWS. 

<img src="Images/AWS_Instance.png">

I have already setup the n8n playbook. The goal here is whenever any alert is triggered in the wazuh manager, we need to fordward the alert to the analyst via messaging applications. If the rule level is less than 7 then only send message to telegram. If rule level is freater than 7 and less than 12 then send message to both telegram and gmail. Else send message to telegram and discord. We also added abusive IP node to check the IP reputation to get the informations about the attacker IP if it is listed in the abusive IP database.

<img width="1920" height="951" alt="image" src="https://github.com/user-attachments/assets/fb3635fc-85b1-4ac8-b3c1-e502d7e1d22e" />

So here the workflow is like when ever an alert is trigged in wazuh the wazuh sends the alert to the n8n webhook. Right after reaching the webhook we will be checking a condition to exclude duplicate alerts. We wont allow the same alert from the same alert trigger twice under 30 minutes. After deduplication we are checking the alert rule levels and based on rule severity we will be sending those alerts to the specific application (i.e, Telegram, Discord and Gmail). I am also pasting the message proof below that indicates the message recieved from the N8N:

<img width="1920" height="951" alt="image" src="https://github.com/user-attachments/assets/09881b63-fe77-4f1a-92a5-fdb8bb204532" />
<img width="1387" height="951" alt="image" src="https://github.com/user-attachments/assets/302a922b-0889-43e5-8913-71b0c36532c8" />
