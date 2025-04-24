---

copyright:

  years: 2023, 2025

lastupdated: "2025-04-24"

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

When you send a share request to an enterprise, you are requesting to add the enterprise to an [allowlist](#x3954001){: term}. After the enterprise accepts the request, you can share individual products and deployable architectures to enterprise users who can create instances of any version that is in the `ready` state. A product is in the `ready` state when it is validated and you've marked it as `ready`. Versions that are not validated are in the `draft` state and are not shared with users. However, unvalidated `draft` versions are available to users who have access to the private catalog that contains the version.

Imagine you are a product manager for the fictitious company _Example Corp_. Your enterprise needs a deployable architecture to provide secure and customizable compute resources for running your applications and services. You browse the {{site.data.keyword.cloud_notm}} catalog and discover the VSI on VPC landing zone option, a deployable architecture that provides the foundation that you need. However, your infrastructure architect decided to [modify the architecture to fully meet your business needs](/docs/secure-enterprise?topic=secure-enterprise-basic-custom). You named your new deployable architecture `Example Corps' infrastructure` and onboarded it to the private catalog `Example Corp catalog`. Now, you are ready to share Example Corps' infrastructure to the rest of your enterprise account `Example Corp enterprise`.

This tutorial uses a fictitious scenario to help you learn and understand how to share a deployable architecture. As you complete the tutorial, adapt each step to match your organization's needs.

## Before you begin
{: #share-custom-prereqs}

1. You must be assigned the Publisher and Viewer access roles for the Catalog Management service to share products with other accounts. For more information, see [Assigning users access](/docs/account?topic=account-catalog-access).

1. [Create a customized deployable architecture](/docs/secure-enterprise?topic=secure-enterprise-basic-custom) called Example Corps' infrastructure. This deployable architecture is the one you will be sharing as you complete this tutorial. 

1. Verify that at least one version of Example Corps' infrastructure is validated and in the `Ready` state. For more information, see [Validating the version](/docs/secure-enterprise?topic=secure-enterprise-onboard-da#validate-version).

## Send a share request
{: #share-request}
{: step}

To send a request to share deployable architectures and products to the enterprise, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Catalogs** > **Private catalogs**.
1. Select **Example Corp catalog**, which is where your deployable architecture is located.
1. Select **Example Corps' infrastructure**.
1. Click **Actions...** > **Share**.
1. Review the list of affected versions. If you don't see the version that you want to share, make sure that the version is in the `ready` state.
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

After the enterprise accepts the request, you need to share the deployable architecture to the enterprise. If your request is rejected, you will need to reach out to the enterprise.

## Contact the enterprise
{: #share-contact}
{: step}

You need to complete this step only if your share request was rejected. Since you are part of the enterprise you are sharing to, you can reach out to the enterprise owner to discuss the share request and discover if changes need to be made.

1. Log in to the enterprise account.
2. Click **Manage** > **Enterprise** > **Accounts**.
3. In the **Accounts** table, find the email of the owner of the enterprise account.
4. Send an email to the owner with details about the share request.

## Share your deployable architecture
{: #share-deployable-architecture}
{: step}

Now that you have permission to share to the enterprise, you can share your deployable architecture. To share the deployable architecture, you need to complete the same steps as sending a share request. To share the deployable architecture, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Catalogs** > **Private catalogs**.
1. Select **Example Corp catalog**, which is where your deployable architecture is located.
1. Select **Example Corps' infrastructure**.
1. Click **Actions...** > **Share**.
1. Review the list of affected versions. If you don't see the version that you want to share, make sure that the version is in the `ready` state.
1. Select **Share to this enterprise or account groups** to see the enterprise and its account groups.
1. Select **Example Corp enterprise** to share to the enterprise and all account groups.
1. Click **Share**.

In the version list, the **Visibility** status is now `Shared`. Users in your enterprise can now [deploy the architecture by using a project](/docs/secure-enterprise?topic=secure-enterprise-deploy-regions). 
