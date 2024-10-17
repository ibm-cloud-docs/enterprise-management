---

copyright:
  years: 2021, 2023
lastupdated: "2024-10-17"

keywords: troubleshooting enterprise iam templates, iam tempalates, enterprise-managed IAM, access enteprise IAM, access templates

subcollection: enterprise-management

---

{{site.data.keyword.attribute-definition-list}}


# Why can't I access enterprise IAM templates?
{: #access-iam-template}
{: troubleshoot}

To view and work with enterprise IAM, you must be in the enterprise account. Users in the enterprise account, including the enterprise account owner, must have either the Template Administrator or Template Assignment Administrator role on All IAM Account Management services.
{: shortdesc}

You get a 403 error when accessing enterprise IAM pages or interacting with the templates and assignments API.
{: tsSymptoms}

The permissions for enterprise IAM templates must be granted explicitly. By default, no users have access to create and assign templates, including the account owner.
{: tsCauses}

The account owner or an administrator can assign a policy with either the Template administrator or Template assignment administrator role on All IAM Account Management services.
{: tsResolve}

1. Go to **Manage > Access (IAM) > Users** and select the user that you want to grant access to.
1. Click **Access > Assign access**.
1. Select **All IAM Account Management services** and click **Next**.
1. Select either the **Template administrator** role, the **Template assignment administrator** role, or both.
1. Click **Next > Review > Add**.
1. Click **Assign**.
