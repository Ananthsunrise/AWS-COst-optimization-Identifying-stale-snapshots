# AWS-COst-optimization-Identifying-stale-snapshots

 In this, we'll create a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.

**Description:**
The Lambda function fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.

**Step 1:
Create an EC2 instance**

Go to aws ec2 -> click launch ec2->select ami as amazon linux2 ami ->select instance type as t2.micro->create new keypair to connect ec2->leave remaining by default and click launch.

**Step 2:
Take a snapshot :** 

Go to aws ec2->go to volumes-select volume which was created by default when ec2 creation-create snapshot

**Step 3:
Create a function in lamda**

Go to lambda->click create function->select python->copy the attached code in this repo and paste in lamda dashboard->click deploy.

**Step 4: 
Give access to lamda to communicate with EBS**

Go to lambda function->click configuration->click permission->click role->click add new policy(create a custom policy and attach that policy)

Custom policy--> select source as ec2 and actions as descripe snapshot, delete snapshot, descripe volume,descripe instances


**Step 5:
To check the working process**

Go to aws ec2 and terminate your ec2 instance. Then volume also deleted automatically.But snapshot is still there.
To delete the snapshot, run the lamda functioon code.   It got deleted.
