# OpsCompass AWS Manual Install Documentation 

## Minimum Requirements: 

1. Admin Access (and ability to create a role) on the Master Account. This will include all accounts for the organization. 

  * Alternative: Admin Access (and ability to create a role) in the account(s) to be scanned. Limited to the accounts that the Admin role has permissions to. 


## General Overview
OpsCompass can begin compliance analysis and drift detection on your company’s environment during one half-hour call with only a few basic requirements to get connected. First, a user needs to be created in AWS. Additionally, the user needs to set up Cloud Trail, create an S3 Bucket, add CloudWatch with specific rules and targets.

## Manual Instructions for Adding AWS Organizations 
* Set up Cloud Trail and name it: `OpsCompass-Trail`
  * Note: Cloud Trail should be setup in the `us-east-1 (N. Virginia)` region

* Select `Create an S3 Bucket` and name it: `opscompass-cloudtrail-[########]`
  * Note: Cloud Trail should be setup in the `us-east-1 (N. Virginia)` region
  
* Configure CloudWatch
  * Swap out `account cloud ID` using **your company account ID**
  * Event Bus Account ID is the `OpsCompass account: 213916962078`
  * Note: CloudWatch rules and targets must be setup in the `us-east-1 (N. Virginia)` region 
 
* Set up a Policy to **Deny S3 Bucket Access** using the following:	



```JSON
{ 
    "Version": "2012-10-17", 
    "Statement": [ 
        { 
            "Sid": "VisualEditor0", 
            "Effect": "Deny", 
            "Action": [ 
                "s3:PutAnalyticsConfiguration", 
                "s3:CreateBucket", 
                "s3:ReplicateObject", 
                "s3:GetBucketObjectLockConfiguration", 
                "s3:DeleteBucketWebsite", 
                "s3:PutLifecycleConfiguration", 
                "s3:PutBucketAcl", 
                "s3:PutObjectTagging", 
                "s3:DeleteObject", 
                "s3:DeleteObjectTagging", 
                "s3:PutAccountPublicAccessBlock", 
                "s3:GetObjectRetention", 
                "s3:PutReplicationConfiguration", 
                "s3:DeleteObjectVersionTagging", 
                "s3:PutObjectLegalHold", 
                "s3:GetObjectLegalHold", 
                "s3:PutBucketCORS", 
                "s3:DeleteBucketPolicy", 
                "s3:PutObject", 
                "s3:GetObject", 
                "s3:PutBucketNotification", 
                "s3:PutBucketLogging", 
                "s3:PutObjectVersionAcl", 
                "s3:PutBucketObjectLockConfiguration", 
                "s3:CreateJob", 
                "s3:PutAccelerateConfiguration", 
                "s3:DeleteObjectVersion", 
                "s3:ReplicateTags", 
                "s3:RestoreObject", 
                "s3:PutEncryptionConfiguration", 
                "s3:GetObjectVersionTorrent", 
                "s3:AbortMultipartUpload", 
                "s3:PutBucketTagging", 
                "s3:UpdateJobPriority", 
                "s3:DeleteBucket", 
                "s3:PutBucketVersioning", 
                "s3:PutObjectAcl", 
                "s3:PutBucketPublicAccessBlock", 
                "s3:PutMetricsConfiguration", 
                "s3:PutObjectVersionTagging", 
                "s3:UpdateJobStatus", 
                "s3:PutInventoryConfiguration", 
                "s3:GetObjectTorrent", 
                "s3:ObjectOwnerOverrideToBucketOwner", 
                "s3:PutBucketWebsite", 
                "s3:PutBucketRequestPayment", 
                "s3:PutObjectRetention", 
                "s3:PutBucketPolicy", 
                "s3:ReplicateDelete", 
                "s3:GetObjectVersion" 
            ], 
            "Resource": "*" 
        } 
    ] 
} 
```

## AWS Setup Process in OpsCompass  
* Click on the link the email from OpsCompass and `Create an Account`

* Click `Add Account` at the bottom of the dashboard in OpsCompass. 

* Click `Add AWS Account` and follow the steps outlined in the green box on the screen.

* Click the 'Create a Role Wizard` link and in the **Permissions** tab Change a Policy from "AdministrativeAccess" to the Managed Policy called "ReadOnlyAccess"

* Create Role 

  * Click into the new role to identify the Role ARN and copy it
  
* Paste the Role ARN into the field within OpsCompass and click "Connect"

OpsCompass will begin to scan the environment. 
