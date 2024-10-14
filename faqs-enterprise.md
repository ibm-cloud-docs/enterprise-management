---

copyright:
  years: 2015, 2024
lastupdated: "2024-10-14"

keywords: account settings, delete account, account errors, reassign account, view tags, batch registration, transfer account ownership

subcollection: secure-enterprise

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}


# FAQs about enterprises
{: #enterprise-faqs}

FAQs for your {{site.data.keyword.cloud}} enterprise might include questions about importing accounts, moving accounts and account groups, and inviting users to your enterprise. To find all FAQs for {{site.data.keyword.cloud_notm}}, see our [FAQ library](/docs/faqs).
{: shortdesc}

## How do I set up an enterprise account?
{: #enterprise-setup}
{: faq}
{: support}

To set up an enterprise, you must be the account owner or an administrator on the Billing account management service. You use the {{site.data.keyword.cloud_notm}} console to create an enterprise account, enter the name of your company, provide your company's domain, create your enterprise structure, and more. For more information, see [Setting up an enterprise](/docs/enterprise-management?topic=enterprise-management-enterprise-tutorial).

## When I create an enterprise, does my {{site.data.keyword.cloud_notm}} account become the enterprise account?
{: #enterprise-account-switch}
{: faq}

No, your {{site.data.keyword.cloud_notm}} account does not become the enterprise account. Your account is added to the enterprise hierarchy. For more information, see [Enterprise hierarchy](/docs/enterprise-management?topic=enterprise-management-what-is-enterprise#enterprise-hierarchy).

## Can I use my {{site.data.keyword.cloud_notm}} account to create multiple enterprise accounts?
{: #enterprise-cloud-account}
{: faq}

No, your {{site.data.keyword.cloud_notm}} account can be a part of only one enterprise account. When you create an enterprise, your account is added to the enterprise hierarchy. See [What is an enterprise?](/docs/enterprise-management?topic=enterprise-management-what-is-enterprise) for more information.

## Can an existing enterprise be a child of another enterprise?
{: #multiple-enterprise}
{: faq}

No, an existing {{site.data.keyword.cloud_notm}} enterprise account can't be imported into another enterprise.

## How do I add child accounts to my enterprise?
{: #enterprise-add-account}
{: faq}

You can use the enterprise dashboard to import an existing account to your enterprise or create a new account within your enterprise. For more information, see [Import existing accounts](/docs/enterprise-management?topic=enterprise-management-enterprise-tutorial&interface=ui#existing_accounts_tutorial) and [Create new accounts](/docs/enterprise-management?topic=enterprise-management-enterprise-tutorial&interface=ui#create-accounts_tutorial).

## Can I import a Lite account into an enterprise?
{: #lite-to-enterprise}
{: faq}

Yes, but your Lite account is automatically upgraded to a Pay-As-You-Go account. Billing for the account is then managed at the enterprise level. For more information, see [Centrally managing billing and usage with enterprises](/docs/enterprise-management?topic=enterprise-management-enterprise).

## Can I remove my account from an enterprise?
{: #remove-enterprise}
{: faq}

After you import your account into an enterprise, you can't remove it.

## Can I move an account within an enterprise?
{: #move-enterprise-account}
{: faq}

Yes, you can move your account anywhere within an enterprise. For example, you can move your account directly under the enterprise or from one account group to another. For more information, see [Moving accounts within the enterprise](/docs/enterprise-management?topic=enterprise-management-enterprise-organize).

## Can I move an account group?
{: #move-account-group}
{: faq}

No, it’s not possible to move an account group within the enterprise.

## Can I edit an account name from within the enterprise?
{: #rename-enterprise-account}
{: faq}

No, you can't edit the name of an account from within your enterprise. To edit the name of an account, go to **Manage** > **Account** in the {{site.data.keyword.cloud_notm}} console, and select **Account settings**. In the Account section, click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit"), enter your new account name, and click **Submit**.

## Can I invite users to an enterprise?
{: #enterprise-invite-users}
{: faq}

To invite users to an enterprise, you must have an {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) access policy with the Editor or higher role on the User Management service. For more information, see [Inviting users](/docs/account?topic=account-iamuserinv&interface=ui#invitations).

## Can my child account have a different subscription currency than my enterprise account?
{: #enterprise-currency}
{: faq}

No, billing and subscriptions are managed at the enterprise level rather than at the child account level. Your child account cannot have a different subscription. For more information about enterprise billing, see [Billing options](/docs/enterprise-management?topic=enterprise-management-enterprise&interface=ui#enterprise-billing-options).

## Can I change the domain for my enterprise account?
{: #enterprise-domain}
{: faq}

Yes, domains can be updated. You can use the [Enterprise Management API](https://{DomainName}/apidocs/enterprise-apis/enterprise#update-enterprise){: external} to update your domain.

## Do individual child accounts receive separate invoices if they are in an enterprise account?
{: #enterprise-invoice}
{: faq}

You can view usage for individual child accounts, but they are not individually invoiced. For more information about enterprise usage, see [Viewing usage in an enterprise](/docs/enterprise-management?topic=enterprise-management-enterprise-usage&interface=ui).

For more information about enterprise billing, see [Centrally managing billing and usage with enterprises](/docs/enterprise-management?topic=enterprise-management-enterprise).

## What account type do I need to create an enterprise account?
{: #enterprise-account-type}
{: faq}

Subscription accounts and Pay-As-You-Go accounts that signed up with a credit card on cloud.ibm.com can create an enterprise account.

## How many child accounts can I have in an enterprise account?
{: #enterprise-account-number}
{: faq}

You can have a maximum of 1000 child accounts that can be distributed across a maximum of 500 account groups. An enterprise can contain up to five tiers of accounts and account groups. For more information, see [Enterprise hierarchy](/docs/enterprise-management?topic=enterprise-management-what-is-enterprise&interface=ui#enterprise-hierarchy)

## Can I create common resources for all of my child accounts?
{: #enterprise-common-resources}
{: faq}

Although you can create resources at the enterprise account level, this method is not a best practice. You can follow best practice by using resource groups and access groups to create and share resources.

For more information, see [Working with resources in an enterprise](/docs/enterprise-management?topic=enterprise-management-enterprise-best-practices#child-resources-enterprise), [Resource management](/docs/enterprise-management?topic=enterprise-management-what-is-enterprise#enterprise-resources), and [Best practices for assigning access](/docs/enterprise-management?topic=enterprise-management-access-enterprises).

## How do I know how many child accounts are in the enterprise as an enterprise account owner?
{: #enterprise-account-count}
{: faq}

To see all accounts within your enterprise, go to your Enterprise dashboard in the console and click **Accounts**.

## Do I automatically have access to child accounts and their resources as an enterprise administrator?
{: #enterprise-admin-access}
{: faq}

No, you do not automatically have access to child accounts and their resources. You need to be invited to individual child accounts and assigned access policies to manage resources. For more information, see [User management for enterprises](/docs/enterprise-management?topic=enterprise-management-enterprise-access-management).

## Can I add users to child accounts as an enterprise administrator?
{: #enterprise-admin-invite}
{: faq}

No, you can't add users to child accounts.

You need to be invited to the child account and assigned the editor or administrator role for the User management service to add users to a child account.

## Do all accounts within an enterprise require the same level of support?
{: #enterprise-acct-support}

Yes, all accounts within an {{site.data.keyword.Bluemix_notm}} enterprise are assigned the same level of support. The level of support that is assigned to an enterprise defaults to the highest support plan within the enterprise. All child accounts within the enterprise also default to the highest support plan.
