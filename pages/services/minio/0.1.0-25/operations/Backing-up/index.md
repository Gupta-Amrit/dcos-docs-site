---
layout: layout.pug
navigationTitle: Back-up
title: Back-up Operation
menuWeight: 30
excerpt: Backing-up Operation of Minio
featureMaturity:
enterprise: false
---

# Backing up

The DC/OS Minio Service allows you to back up your data to AWS S3 compatible storage. For backing up data to AWS S3 compatible bucket, DC/OS Minio uses ‘mc mirror’ command. Minio provides a ‘rsync’ like command line utility. It mirrors data from one bucket to another. The following information and values are required to back up your data.

    1. ACCESS_KEY_ID
    2. SECRET_ACCESS_KEY
    
To enable backup, trigger the backup-S3 Plan with the following plan parameters:
```shell
{
 'ACCESS_KEY_ID': access_key_id,
 'SECRET_ACCESS_KEY': secret_access_key
}
``` 

Plans are executed in DC/OS with the following command:
```shell
{
 dcos miniod --name=<service_name> plan start <plan_name> -p <plan_parameters>
}
```
For launching backup-s3 plan, issue the below command with the requisite parameters:

```shell
{
 dcos miniod --name=<SERVICE_NAME> plan start backup-s3 \
  -p ACCESS_KEY_ID=<ACCESS_KEY> \
  -p SECRET_ACCESS_KEY=<SECRET_ACCESS_KEY>
}
````

Once this plan is executed, the backup will be uploaded to S3 compatible storage.

Backup will be performed using three sidecar tasks:

1. `Init Task` - A separate Pod will be started at any Private Agent. An init task will be responsible to register both Minio as well as S3 compatible client.

[<img src="../../img/Init_task.png" alt="Init_task" width="800"/>](../img/Init_task.png)

   _Figure 1. - Register Minio and S3 client

2. `Delete-Previous-Snapshot` - This task is responsible to delete the buckets in the AWS S3 compatible storage which were deleted in the DC/OS Minio since the last backup.

[<img src="../../img/Delete_Previous_Snapshot.png" alt="Delete_Previous_Snapshot" width="800"/>](../img/Delete_Previous_Snapshot.png)

   _Figure 2. - Delete previous backup
   
3. `Backup Task` - The Backup task is responsible for making a backup of the data in the DC/OS Minio storage to the AWS S3 compatible storage. A backup task will run the ‘mc mirror’ command by taking ACCESS_KEY_ID and SECRET_ACCESS_KEY as parameters.
It will create new buckets in AWS S3 compatible storage according to the current snapshot or state of Minio storage system.

[<img src="../../img/Backup.png" alt="Backup" width="800"/>](../img/Backup.png)

   _Figure 3. - Backing Up to S3 compatible storage
   
'backup-s3' plan would execute all the three aforementioned tasks serially. 

