# Exporting AWS RDS Snapshot to S3 #


### What is this repository for? ###

* Setting up SSH Tunnel to AWS RDS DB instance
in a private subnet
* Using MySQL Workbench to connect to RDS DB instance
* Taking RDS Snapshot
* Exporting RDS Snapshot to destinated S3 bucket

### SSH Tunnel to AWS RDS DB Instance ###

![DB-instance1](DB_instance_Creation3.png)

#### Step 1: Deploy AWS RDS instance ####

![DB-instance2](/img/DB_instance_Creation.png)

#### Step 2: Configure the AWS RDS instance ####

![DB-instance3](/img/DB_instance_Creation2.png)

![DB-instance4](/img/DB_instance_Creation4.png)

#### Step 2a: Specify DB instance name & username, password ####

![DB-instance5](/img/DB_instance_Creation5.png)

![DB-instance6](/img/DB_instance_Creation6.png)

![DB-instance7](/img/DB_instance_Creation7.png)

#### Step 2b: Specify connectivity configuration of the DB instance ####

![DB-instance8](/img/DB_instance_Creation8.png)

#### DB instance Deployed ####

![DB-instance12](/img/DB_instance_Creation12.png)


#### Step 3: Deploy EC2 instance - Bastion Host within the same VPC ####

![EC2-instance1](/img/EC2-instance1.png)

#### Created EC2 keypair for EC2 instance ####

![EC2-instance2](/img/EC2-instance2.png)

#### Bastion Host Deployed within the same VPC as RDS DB instance ####

![EC2-instance3](/img/EC2-instance3.png)

#### Add the Bastion Host security group to the RDS inbound rules ####

![DB-RDS-SSH](/img/SSH-Tunnel.png)

![DB-instance-final](/img/DB_instance_Creation11.png)

#### Step 4: Use MySQL Workbench to created SSH Tunnel to RDS Instance ####


![EC2-instance-IP](/img/EC2-instance4.png)

![DB-Endpoint](/img/DB_instance_Creation9.png)

#### Add the EC2 public IP and RDS endpoint in MySQL Workbench ####

![DB-instance-10](/img/DB_instance_Creation10.png)

![MySQL-workbench1](/img/MySQLWorkbench2.png)

#### Populate the RDS DB instance ####

![MySQl-workbench2](/img/MySQLWorkbench3.png)

#### Step 5: Export the RDS snapshot to S3 bucket ####

* First take DB snapshot of the RDS DB instance

![DB-snapshot](/img/DB_instance_snapshot1.png)

* Select the DB snapshot and then select Export to S3

![DB-snapshot2](/img/DB_instance_snapshot2.png)

* Create an S3 bucket for the destinated bucket to store exported DB snapshot

![DB-snapshot3](/img/DB_instance_snapshot3.png)

* Select the S3 bucket created to store the exported DB snapshot

![Exported1](/img/Exports1.png)

* Create a new IAM role that provides permission to RDS instance to access S3 for export

![Exported2](/img/Exports2.png)

* The IAM role created for RDS export to S3

![IAM-role](/img/IAM_role_exports.png)

* Create the Customer Managed Keys for export

![CMK1](/img/KMS_Customer_Managed1.png)

![CMK2](/img/KMS_Customer_Managed2.png)

![CMK3](/img/KMS_Customer_Managed3.png)


#### Final Result of Exported Snapshot in S3 Bucket ####

![S3-Bucket1](/img/S3-bucket1.png)

![S3-Bucket2](/img/S3-bucket2.png)

#### Apache Parquet format for Exported DB snapshot ####

![S3-Bucket3](/img/S3-bucket3.png)

---------------------------------------------------------

## AWS RDS DB restore from snapshot (backup) ##

![DB-restore](/img/DB-restore1.png)

![DB-restore2](/img/DB-restore2.png)

![DB-restore3](/img/DB-restore3.png)

![DB-restore4](/img/DB-restore4.png)

### AWS RDS DB instance is restored from the snapshot ###

![DB-restore5](/img/DB-restore5.png)

![DB-restore6](/img/DB-restore6.png)

### Updated MySQL Workbench client with the new RDS endpoint to connect ###

![DB-restore7](/img/DB-restore7.png)

### Now able to successfully connect to the restored DB instance and see MySQL queries ###

![DB-restore8](/img/DB-restore8.png)
