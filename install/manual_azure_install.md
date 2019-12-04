# OpsCompass Azure Manual Install Documentation 

## Minimum Requirements: 

1. Azure AD Global Admin to authorize the `opscompass` Enterprise Application (service principal)  
1. Owner Role or Write Role Permission on Monitored Subscriptions 

	* Write Role Assignments 
	
	* Write Policy Definitions 
	
	* Write Policy Assignments 

## General Overview
OpsCompass can begin compliance analysis and drift detection on your company’s environment during one half-hour call with only a few basic requirements to get connected. First, a service principal needs to be created in Azure Active Directory; this part of the setup requires the authorization of a Global Admin on the target tenant. The second, and final requirement to connect OpsCompass is for an owner of the desired subscription(s) to simply add the account to our product to begin monitoring.

## Manual Instructions for Adding Azure Subscriptions 
* For each subscription in the tenant, navigate to Access Control (IAM) and add `opscompass` as a Contributor or use Azure CLI.  
	
* Set up an IAM Policy to write policy definitions and policy assignments by placing the following json in a file named `opscompass.json`, replacing `${subscriptionId}` with the ID of the subscription you're adding.	

```JSON
{ 
    "Name": "OpsCompassPolicy-${subscriptionId}", 
    "IsCustom": true, 
    "Description": "OpsCompass Policy Administration", 
    "Actions": [ 
        "microsoft.authorization/policydefinitions/write", 
        "microsoft.authorization/policyassignments/write" 
    ], 
    "AssignableScopes": [ 
        "/subscriptions/${subscriptionId}" 
    ] 
  } 
```

* Run the following command in Azure CLI to create the policy: 
```CMD
az policy definition create  -n "OpsCompassPolicy-${subscriptionId}" --params opscompass.json
```

* For each subscription, go to IAM and create an assignment for the new OpsCompassPolicy-${subscriptionId} and apply it to the `opscompass` service principal.  

* Navigate back to [helm.opscompass.com](https://helm.opscompass.com) and “Add Account” (located at the bottom of the dashboard). You will be asked to re-enter the tenant ID just like during initial setup but this time OpsCompass will pull in the subscriptions. 
