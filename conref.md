---

copyright:
   years: 2024
lastupdated: "2025-01-08"

keywords:

subcollection: enterprise-management

content-type: conref

---


{{site.data.keyword.attribute-definition-list}}

# Content references for billing-usage subcollection
{: #conref-billing}

Reuse sections within the billing-usage repo.
{: shortdesc}
{: #my-shortdesc-reuse}

H1's would never be able to be reused. Each Markdown file can only ever have one H1. However, any H2-H6 can be fully reused.


To view usage for an on-premises resource, like {{site.data.keyword.powerSys_notm}} Privae Cloud, filter the **Pricing region** column to the {{site.data.keyword.satelliteshort}} location associated with your pod. Then, filter the **Service name** column to {{site.data.keyword.powerSys_notm}}.
{: #on-prem-commit}

Map commitment usage in your enterprise back to child accounts by completing the following steps:
1. Go to the **Entity ID** column and filter on an account ID.
1. Go to the **Service name** column and filter on the service that is associated with your commitment. The sum of the **Cost** column gives you this month's usage towards a service-level commitment in a specific account.
{: #enterprise-commit}
