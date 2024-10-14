---

copyright:

  years: 2019, 2024

lastupdated: "2024-10-14"

keywords: enterprise access

subcollection: secure-enterprise

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
