# Task-to-practice
1. As part of the temporary assignment to the Nautilus project, a developer named siva requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed. Here's what you need to do:
Create a user named siva on App Server 2 in Stratos Datacenter. Set the expiry date to 2023-12-07, ensuring the user is created in lowercase as per standard protocol.

A: ✅ Step 1: SSH into App Server 2
ssh user@appserver2   # replace 'user' with your login
✅ Step 2: Create the user siva with expiry
sudo useradd -e 2023-12-07 siva
-e → expiry date (format: YYYY-MM-DD).
siva → username (lowercase, per your requirement).
✅ Step 3: Set a password (if required)
sudo passwd siva
sudo grep siva /etc/shadow
✅ Step 4: Verify user expiry
sudo chage -l siva
You should see something like:
Account expires    : Dec 07, 2023
Password expires   : never
⚡ Done! The user siva will exist but will automatically expire on 2023-12-07.

2. create user with non-interactive shell
A: sudo useradd -s /sbin/nologin stev
grep stev /etc/passwd

3. Following security audits, the Fusion Industries security team has rolled out new protocols, including the restriction of direct root SSH login.
Your task is to disable direct SSH root login on all app servers within the Strar Datacenter.
A: SSH into each App Server
ssh user@appserverX   # replace user and X with correct details
Open the SSH daemon configuration
sudo vi /etc/ssh/sshd_config
Find and update the following line
PermitRootLogin no
If it’s set to yes, change it to no.
If it’s commented (#PermitRootLogin yes), uncomment and set it to no.
Restart SSH service
# On most systems
sudo systemctl restart sshd
# On some older systems
sudo service sshd restart
Verify
ssh root@appserverX
It should now say Permission denied.
