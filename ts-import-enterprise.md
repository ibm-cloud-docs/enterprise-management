---

copyright:
  years: 2015, 2023
lastupdated: "2024-10-17"

keywords: troubleshoot enterprise, enterprise problem, import enterprise, existing enterprise

subcollection: enterprise-management

content-type: troubleshoot
---

{{site.data.keyword.attribute-definition-list}}


# Why can't I import an existing account to the enterprise?
{: #troubleshoot-existing-enterprise}
{: troubleshoot}

To import an existing enterprise, you must have the correct access roles assigned on the Billing service.
{: shortdesc}

When you try to import an existing account to enterprise, one of the following issues occurs:
{: tsSymptoms}

* When you click **Add existing account** in the Account section in the console, the account that you want to add is not listed.
* You don't have the option to click **Import account**.

You aren't assigned the correct access, or the account isn't eligible to be imported.
{: tsCauses}

If you can't see the existing account that you want to import, you need the Administrator role on the Billing service of the existing account.
{: tsResolve}

If the **Import account** option isn't available, verify that you have the Administrator or Editor role on the Billing service of the enterprise and the Administrator or Editor role on the Enterprise service for the parent enterprise or account group.

If the account that you want to import is a Pay-As-You-Go account and you're still unable to import it after you verify that you have access, the account might not be eligible to be imported into the enterprise. Some Pay-As-You-Go accounts can't be directly imported into an enterprise, such as many Pay-As-You-Go accounts that are billed in United States dollars (USD). Contact [{{site.data.keyword.Bluemix_notm}} Sales](https://www.ibm.com/cloud?contactmodule){: external} to convert the account to a Subscription account, and then import it into the enterprise.
