---

copyright:

  years: 2019, 2025

lastupdated: "2025-08-11"

keywords: enterprise access

subcollection: enterprise-management

---

{{site.data.keyword.attribute-definition-list}}

# User management for enterprises
{: #enterprise-access-management}

{{site.data.keyword.cloud}} enterprises are valuable for large companies or organizations that need to group a set of accounts while still maintaining a separation and isolation between the accounts for different departments or teams. For more information about enterprises, see [What is an enterprise?](/docs/enterprise-management?topic=enterprise-management-what-is-enterprise)
{: shortdesc}

With the correct access in an enterprise account, you can use enterprise-managed IAM templates to centrally administer IAM resources, like access groups, trusted profiles, and settings, for child accounts. Users who have the Template Administrator and Template Assignment Administrator roles on **All IAM Account Management services** can efficiently manage access to IAM-enabled resources in child accounts. Plus, as an IAM administrator in child accounts, you can still create your own IAM resources to stay flexible with your needs.

Assigning IAM resources to accounts and account groups is an efficient way to grant standardized access to users in child accounts and reduce policy drift. For more information, see [How enterprise-managed IAM access works](/docs/enterprise-management?topic=enterprise-management-access-enterprises&interface=ui#how-enterprise-iam).

The user list for each child account in an enterprise is accessible only to users in that child account. This means the users who are invited to the enterprise and the users who are invited to the accounts within the enterprise remain entirely separate. This is beneficial because you can add multiple accounts to an enterprise and organize them as needed into account groups, but keep the user lists restricted from other accounts.

In most cases, you want to add only the users to your enterprise account that need the ability to manage the enterprise. Depending on the role the user is assigned on the [Enterprise account management service](/docs/account?topic=account-account-services#enterprise-account-management), they have varying levels of access for managing the enterprise. For example, a user assigned the Administrator role on the Enterprise service can rename the enterprise, update the domain, view usage, create accounts, and more. However, a user with the viewer or operator role is limited to viewing the accounts and account groups hierarchy for the enterprise.

Inviting users to the enterprise account doesn't provide access to manage any of the child accounts within the enterprise or their resources. If you add a user to an enterprise account that contains a number of accounts, those users do not automatically have access to manage those accounts as far as user management, billing, and more. The enterprise account users also don't have access to any resources in other accounts within the enterprise.

If you want a user to manage the enterprise and have access to resources within child accounts, you must invite them to both accounts. Assigning access policies in the enterprise account allows the user to manage the enterprise. And, assigning access policies within the child account allows the user to manage specific resources or complete account management tasks within that account only.
{: note}

For information about assigning access to users in an enterprise, see [Assigning access for enterprise management](/docs/enterprise-management?topic=enterprise-management-assign-access-enterprise).

## Setting up centralized access to manage enterprise audit logs
{: #enterprise-audit-logs}

Enterprise customers can create authorization policies that allow log instances in multiple accounts to send logs to a centralized log instance, that uses just one policy. This is achieved by specifying a broader scope, either the entire enterprise or a specific account group while defining the subject of the policy.

While setting up access to forward logs from multiple accounts to a centralized logging instance, the authorization policy includes:

* Subject: Defines the scope of the logs. which can be one of the following:
  * An enterprise ID - applies to all accounts in an enterprise.
  * An account group ID - applies to all accounts within that specific group.
  * A specific account ID - applies only to an account.
* Service: Both the source and target services are typically set to `logs`.
* Resource: Identifies the centralized log instance that receives logs.
* Role: Grants permissions such as `writer` or `sender` to allow log forwarding.

### Core benefits
{: #core-benefits}

The core benefits of this approach provides centralized, scalable, and efficient access control across your enterprise environment, including:

* Single-point access control - one policy covers multiple accounts.
* Automatic coverage - new accounts that are added to the enterprise or group are included without extra configuration.
* Simplified management - reduces the number of policies that are required and streamlines access setup across environments.

### Example scenarios
{: #example-scenarios}

Platform attributes for scoping authorization by enterprise ID or account group ID.

If an enterprise ID is specified in the policy, all log instances in child accounts within the enterprise sends logs to the centralized log instance. This setup simplifies configuration by requiring only one policy, regardless of the number of accounts involved.

If an account group ID is used, all log instances within accounts grouped under that specific ID are allowed to send logs to the central instance. Additionally, any accounts added to the group in future are automatically included, ensuring seamless and scalable log integration.

#### Enterprise ID example
{: #enterprise-example}

The following example shows how attributes in authorization policies indicate a subject’s resource within the scope of an enterprise.

```java
{
   "type": "authorization",
   "subject": {
       "attributes": [
        {
           "key": "enterpriseId",
           "operator": "stringEquals",
           "value": "$ENTERPRISE_ID"
        },
        {
           "key": "serviceName",
           "operator": "stringEquals",
           "value": "$SERVICE_NAME"
        }
       ]
   },
   "control": {
      "grant": {
        "roles": [
        {
          "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Writer"
        }
      ]
     }
  },
  "resource": {
      "attributes": [
      {
         "key": "accountId",
         "operator": "stringEquals",
         "value": "$ACCOUNT_ID"
      },
      {
         "key": "serviceName",
         "operator": "stringEquals",
         "value": "$SERVICE_NAME"
      },
      {
         "Key": "serviceInstance",
         "operator": "stringEquals",
         "value": "SERVICE_INSTANCE_ID"
      }
   ]
  }
}
```
{: codeblock}
{: java}

#### Account group ID example
{: #account-example}

The following example shows how attributes in authorization policies indicate a subject's resource within the scope of an account group.

```java
{
   "type": "authorization",
   "subject": {
       "attributes": [
        {
           "key": "AccountGroupId",
           "operator": "stringEquals",
           "value": "$ENTERPRISE_ACCOUNT_GROUP_ID"
        },
        {
           "key": "serviceName",
           "operator": "stringEquals",
           "value": "$SERVICE_NAME"
        }
      ]
    },
    "control": {
       "grant": {
         "roles": [
        {
           "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Writer"
        }
      ]
    }
  },
    "resource": {
       "attributes": [
      {
         "key": "accountId",
         "operator": "stringEquals",
         "value": "$ACCOUNT_ID"
      },
      {
         "key": "serviceName",
         "operator": "stringEquals",
         "value": "$SERVICE_NAME"
      },
      {
         "Key": "serviceInstance",
         "operator": "stringEquals",
         "value": "SERVICE_INSTANCE_ID"
      }
    ]
  }
}
```
{: codeblock}
{: java}
