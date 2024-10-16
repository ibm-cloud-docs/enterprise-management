---

copyright:
  years: 2021, 2023
lastupdated: "2024-10-16"

keywords: troubleshooting enterprise iam templates, iam tempalates, enterprise-managed IAM, access enteprise IAM, access templates

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}


# Why can't I see any child accounts when I'm assigning an enterprise IAM template?
{: #view-child-accounts}
{: troubleshoot}

To view and select accounts for assignment, you must have the Administrator role on the Enterprise service.
{: shortdesc}

When you go to assign an enterprise IAM template, you can't view the child accounts in the enterprise.
{: tsSymptoms}

You don't have the Administrator role on the Enterprise service.
{: tsCauses}

The account owner or an administrator on the Enterprise service can assign to you a policy with the Administrator role on the Enterprise service.
{: tsResolve}

1. Go to **Manage > Access (IAM) > Users** and select the user that you want to grant access to.
1. Click **Access > Assign access**.
1. Select **Enterprise** and click **Next**.
1. Select the Administrator role.
1. Click **Next > Review > Add**.
1. Click **Assign**.
