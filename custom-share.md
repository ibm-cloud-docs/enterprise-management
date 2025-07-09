---

copyright:

  years: 2023, 2025

lastupdated: "2025-07-09"

keywords: deployable architecture, custom, share, enterprise

subcollection: enterprise-management

content-type: tutorial
account-plan: paid
completion-time: 5m

---

{{site.data.keyword.attribute-definition-list}}

# Sharing your deployable architecture to your enterprise
{: #share-custom}
{: toc-content-type="tutorial"}
{: toc-completion-time="5m"}

This tutorial walks you through how to share a deployable architecture that you created from an {{site.data.keyword.cloud}} pre-built deployable architecture. By completing this tutorial, you learn about sending a share request, viewing the status of your share request, and sharing your deployable architecture.
{: shortdesc}

When you send a share request to an enterprise, you are requesting to add the enterprise to an [allowlist](#x3954001){: term}. After the enterprise owner [accepts the request](/docs/enterprise-management?topic=enterprise-management-catalog-share-accept&interface=ui#prereqs-enterprise-share), you can share individual products and deployable architectures to enterprise users. You can share any version that is in the `ready` or `pre-release` state. For more information on states, go to [Versioning workflow in your private catalog](/docs/account?topic=account-catalog-share-overview#version-flow). 

Not ready to share your deployable architecture, or are you not a part of an enterprise? You can skip this tutorial and continue on to [deploying an architecture by using a project](/docs/secure-enterprise?topic=secure-enterprise-deploy-regions). Users in your account who have access to the private catalog that contains a `draft` version of your deployable architecture can deploy it. 
{: tip}

Imagine you are a product manager for the fictitious company _Example Corp_. Your enterprise needs a deployable architecture to provide secure and customizable compute resources for running your applications and services. Your infrastructure architect browsed the {{site.data.keyword.cloud_notm}} catalog and discovered the Cloud automation for {{site.data.keyword.codeengineshort}} option, a deployable architecture that provides the foundation that you need. However, your infrastructure architect decided to [modify the architecture to fully meet your business needs](/docs/secure-enterprise?topic=secure-enterprise-basic-custom). Your cloud automation engineering professional named your new deployable architecture `Example Corp's infrastructure` and onboarded it to the private catalog `Example Corp catalog`. Now, you are ready to share `Example Corp's infrastructure` to the rest of your enterprise account `Example Corp enterprise`.

This tutorial uses a fictitious scenario to help you learn and understand how to share a deployable architecture. As you complete the tutorial, adapt each step to match your organization's needs.

## Before you begin
{: #share-custom-prereqs}

1. You must be assigned the Publisher and Viewer access roles for the Catalog Management service to share products. For more information, see [Assigning users access](/docs/account?topic=account-catalog-access).

1. Verify that your account is part of an enterprise. You can create an enterprise from an existing Subscription account or a qualifying Pay-as-you-Go account. For more information, go to [Creating an enterprise](/docs/enterprise-management?topic=enterprise-management-create-enterprise&interface=ui).

1. [Create a customized deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-basic-custom) called `Example Corp's infrastructure` and onboard it to a private catalog called `Example Corp catalog`. This deployable architecture is the one you will be sharing as you complete this tutorial. 

1. Verify that at least one version of `Example Corp's infrastructure` is in the `ready`, `test`, or `pre-release` state. For more information on states, go to [Versioning workflow in your private catalog](/docs/account?topic=account-catalog-share-overview#version-flow).

## Send a share request
{: #share-request}
{: step}

To send a request to share deployable architectures and products to the enterprise, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Catalogs** > **Private catalogs**.
1. Select **Example Corp catalog**, which is where your deployable architecture is located.
1. Select **Example Corp's infrastructure**.
1. Click **Actions** > **Share**.
1. Review the list of affected versions. If you don't see the version that you want to share, make sure that the version is in the `ready`, `test`, or `pre-release` state.
1. Select **Share to this enterprise or account groups** to see the enterprise and its account groups.
1. Select **Example Corp enterprise** to share to the enterprise and all account groups.
1. Click **Share**.

In the version list, the **Visibility** status is now `Pending`. Next, the enterprise needs to accept the share request. For more information, see [Accepting share requests for private catalog products](/docs/enterprise-management?topic=enterprise-management-catalog-share-accept).

## Check the share request status
{: #share-status}
{: step}

You can check the share request status by completing the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, select **Manage** > **Catalogs** > **Share requests**.
2. Click **Sent requests** to show the table of all your requests.
   - If the enterprise accepted the request, the request state is `Accepted`.
   - If the enterprise denied the request, the request state is `Rejected`.

After the enterprise accepts the request, your deployable architecture is shared with the enterprise. If your request is rejected, you need to reach out to the enterprise owner.

## Contact the enterprise
{: #share-contact}
{: step}

You need to complete this step only if your share request is rejected. Since you are part of the enterprise you are sharing to, you can reach out to the enterprise owner to discuss the share request and discover if changes need to be made.

1. Log in to the enterprise account.
2. Click **Manage** > **Enterprise** > **Accounts**.
3. In the **Accounts** table, find the email of the owner of the enterprise account.
4. Send an email to the owner with details about the share request.

After the request is accepted, the **Visibility** status is now `Shared` in the version list. Users in your enterprise can now [deploy the architecture by using a project](/docs/secure-enterprise?topic=secure-enterprise-deploy-regions). 
