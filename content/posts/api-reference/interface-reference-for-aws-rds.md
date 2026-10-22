---
title: "Interface Reference for AWS RDS"
date: 2022-08-16T08:40:15+00:00
draft: false
---

This Interface Reference for AWS RDS API covers how to create an RDS instance using the Python SDK library Boto3. RDS supports many DB engines, but the examples will focus on the MySQL db. The interface will programmatically invoke an API call to create a MySQL database. The Reference will also cover how to stop the database as you will incur costs if you keep it running. The methods covered here are `create_db_instance` and `stop_db_instance`.

**Get Started**

**Prerequisites**

- AWS account

- Python 3.7 or later is required

- **Creates** a new DB instance.
The new DB instance is a RDS DB instance.

```
`CreateDBInstance`
```

**Request parameters**

The *API Reference* covers only a few request parameters. For a detailed list, refer to the *AWS [RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/ProgrammingGuide.html)* docs.

Property name**Type**Required**Description**AllocatedStorage IntegerNoThe amount of storage in gibibytes (GiB) to allocate for the DB instance.
DBInstanceClassStringYesThe compute and memory capacity of the DB instance, for example db.m5.large.DBInstanceIdentifierStringYesThe DB instance identifierEngineStringYesThe name of the database engine to be used for this instance.MasterUserPasswordStringNoThe password for the master user.MasterUsernameStringNoThe name for the master user.

**Example**

Sample code snippet to create an RDS instance for MySQL DB using the Python SDK library boto3.

```
`import boto3

client = boto3.client('rds')

response = client.create_db_instance(
    AllocatedStorage=5,
    DBInstanceClass='db.t2.micro',
    DBInstanceIdentifier='database-instance-01',
    Engine='MySQL',
    MasterUserPassword='testjanetj123',
    MasterUsername='janet89',
)

print(response)`
```

**Response**

From the terminal, run the command to see the output. 

```
`python3 dbConn.py`
```

Confirm that you have configured aws on your terminal as the credentials are stored in the config files. You will get an error if the keys are not saved.

![](/images/interface-reference-for-aws-rds/startdb.png)

Check the AWS RDS service on the Management Console to confirm that the DB instance is getting instantiated.

![](/images/interface-reference-for-aws-rds/dbinstance.png)

This is the formatted JSON output retrieved from the terminal.

```
`{
   "DBInstance":{
      "DBInstanceIdentifier":"database-instance-01",
      "DBInstanceClass":"db.t2.micro",
      "Engine":"mysql",
      "DBInstanceStatus":"creating",
      "MasterUsername":"janet89",
      "AllocatedStorage":5,
      "PreferredBackupWindow":"06:24-06:54",
      "BackupRetentionPeriod":1,
      "DBSecurityGroups":[
         
      ],
      "VpcSecurityGroups":[
         {
            "VpcSecurityGroupId":"sg-0e14e35a9046aa2f5",
            "Status":"active"
         }
      ],
      "DBParameterGroups":[
         {
            "DBParameterGroupName":"default.mysql8.0",
            "ParameterApplyStatus":"in-sync"
         }
      ],
      "DBSubnetGroup":{
         "DBSubnetGroupName":"default",
         "DBSubnetGroupDescription":"default",
         "VpcId":"vpc-0c8f2d6d0323e45fc",
         "SubnetGroupStatus":"Complete",
         "Subnets":[
            {
               "SubnetIdentifier":"subnet-0e52c40e45adbb3ce",
               "SubnetAvailabilityZone":{
                  "Name":"us-east-1f"
               },
               "SubnetOutpost":{
                  
               },
               "SubnetStatus":"Active"
            },
            {
               "SubnetIdentifier":"subnet-086db67d473e5893f",
               "SubnetAvailabilityZone":{
                  "Name":"us-east-1d"
               },
               "SubnetOutpost":{
                  
               },
               "SubnetStatus":"Active"
            },
            {
               "SubnetIdentifier":"subnet-0d20532929cab0a83",
               "SubnetAvailabilityZone":{
                  "Name":"us-east-1c"
               },
               "SubnetOutpost":{
                  
               },
               "SubnetStatus":"Active"
            },
            {
               "SubnetIdentifier":"subnet-0417c5329441f6123",
               "SubnetAvailabilityZone":{
                  "Name":"us-east-1e"
               },
               "SubnetOutpost":{
                  
               },
               "SubnetStatus":"Active"
            },
            {
               "SubnetIdentifier":"subnet-016a722e3bfb5ba9a",
               "SubnetAvailabilityZone":{
                  "Name":"us-east-1b"
               },
               "SubnetOutpost":{
                  
               },
               "SubnetStatus":"Active"
            },
            {
               "SubnetIdentifier":"subnet-0bc9068fd92a18040",
               "SubnetAvailabilityZone":{
                  "Name":"us-east-1a"
               },
               "SubnetOutpost":{
                  
               },
               "SubnetStatus":"Active"
            }
         ]
      },
      "PreferredMaintenanceWindow":"wed:05:23-wed:05:53",
      "PendingModifiedValues":{
         "MasterUserPassword":"****"
      },
      "MultiAZ":false,
      "EngineVersion":"8.0.28",
      "AutoMinorVersionUpgrade":true,
      "ReadReplicaDBInstanceIdentifiers":[
         
      ],
      "LicenseModel":"general-public-license",
      "OptionGroupMemberships":[
         {
            "OptionGroupName":"default:mysql-8-0",
            "Status":"in-sync"
         }
      ],
      "PubliclyAccessible":true,
      "StorageType":"gp2",
      "DbInstancePort":0,
      "StorageEncrypted":false,
      "DbiResourceId":"db-OK7HY5OY4LJYXHVJYTTCY6NAVE",
      "CACertificateIdentifier":"rds-ca-2019",
      "DomainMemberships":[
         
      ],
      "CopyTagsToSnapshot":false,
      "MonitoringInterval":0,
      "DBInstanceArn":"arn:aws:rds:us-east-1:597956760726:db:database-instance-01",
      "IAMDatabaseAuthenticationEnabled":false,
      "PerformanceInsightsEnabled":false,
      "DeletionProtection":false,
      "AssociatedRoles":[
         
      ],
      "TagList":[
         
      ],
      "CustomerOwnedIpEnabled":false,
      "BackupTarget":"region",
      "NetworkType":"IPV4"
   },
   "ResponseMetadata":{
      "RequestId":"31127859-2c52-45bc-896a-b6eb2ab5bb23",
      "HTTPStatusCode":200,
      "HTTPHeaders":{
         "x-amzn-requestid":"31127859-2c52-45bc-896a-b6eb2ab5bb23",
         "content-type":"text/xml",
         "content-length":"5036",
         "date":"Fri, 12 Aug 2022 21:09:25 GMT"
      },
      "RetryAttempts":0
   }
}`
```

2. **Stops** an Amazon RDS DB instance.

```
`StopDBInstance`
```

**Request parameters**

Property name**Type**Required**Description**DBInstanceIdentifierStringYesThe DB instance identifier

**Example**

Sample Python SDK for stopping the instance.

```
`import boto3

client = boto3.client('rds')

response = client.stop_db_instance(
    DBInstanceIdentifier='database-instance-01'
)
print(response)`
```

**Response**

The response shows the parameter `DBInstanceStatus:stopping`. It may take a few minutes before it displays as `stopped`.

![](/images/interface-reference-for-aws-rds/stopdb.png)

The Console will update the DB instance as stopped once it terminates the database.

![](/images/interface-reference-for-aws-rds/stopdbinstance.png)
