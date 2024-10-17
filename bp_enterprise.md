---

copyright:
  years: 2019, 2023
lastupdated: "2024-10-17"

keywords: enterprise, enterprise resources, enterprise account, best practices, setting up an enterprise

subcollection: enterprise-management

---

{{site.data.keyword.attribute-definition-list}}


# Best practices for setting up an enterprise
{: #enterprise-best-practices}

These best practices provide you with the basic building blocks for setting up an {{site.data.keyword.cloud}} enterprise. You can also review the [Enterprise account architecture](/docs/enterprise-account-architecture) white paper to learn about how you can take advantage of automation and the recommendations for how large customers should configure and govern {{site.data.keyword.cloud_notm}} at scale.
{: shortdesc}

## Organizing accounts according to how you want to track billing
{: #organize-enterprise-usage}

A key benefit of {{site.data.keyword.cloud_notm}} enterprises is that they enable you to centrally view and manage billing and usage across multiple accounts. This capability's usefulness depends on your enterprise structure because usage data is aggregated by each account group and account. Create account groups for projects that function under a common budget. See [How can I use an enterprise?](/docs/enterprise-management?topic=enterprise-management-what-is-enterprise#enterprise-use-cases) for examples.

The enterprise administrator or your financial officer might not be familiar with each individual account or account group. To make it easier to identify their purpose, give each account and account group a human-readable name. If your company uses billing codes, you can also incorporate them into the name. For example, instead of a `devteam` account group with `fed ui` and `be api` accounts, create the `Development - A2B3` account group with `Front-end UI team` and `Back-end API team` accounts.

An enterprise user with Administrator or Editor access can edit the enterprise and account group names, but they can't change account names. To edit an account name, a user must be in the account itself.
{: tip}

Because you have a unified view of all usage that's organized by your account groups and accounts, you can charge back usage costs to the associated teams. For more information, see [Recovering costs for enterprise usage](/docs/enterprise-management?topic=enterprise-management-enterprise-usage&interface=ui#enterprise-cost-recovery).

## Creating a consistent enterprise hierarchy
{: #accounts-vs-groups}

When you set up your enterprise, you create an enterprise hierarchy that reflects your company or organization. Reference the [Enterprise account architecture](/docs/enterprise-account-architecture) white paper to learn about taking advantage of automation and the recommendations for how to configure and govern {{site.data.keyword.cloud_notm}} at scale.

As you create accounts and account groups, plan a consistent scheme for how your company uses the following enterprise layers:

- Resource groups
- Accounts within an account group
- Account groups within the enterprise

For example, your company might create accounts for each team, with resource groups or projects within the account for development, testing, and production environments. Another company might have distinct accounts for each environment, which are grouped into account groups for each team.

However you choose to structure your enterprise, be as consistent as possible to simplify enterprise management. Because it's easy to create and keep track of new accounts, it can be tempting to create many separate accounts as users request them. However, each account introduces more management overhead. As you plan how to structure your enterprise, keep in mind the following points:

- For each account that you create, users must be invited and their access must be managed separately or with [enterprise-managed IAM templates](/docs/enterprise-management?topic=enterprise-management-access-enterprises).
- An inconsistent structure can make it harder to determine who to give access within each account and which teams are using resources.
- Users can collaborate on resources and services within an individual account only. Resources can't be moved between accounts.

## Setting up access policies in an enterprise
{: #access-enterprise}

As always, follow the best practice for assigning the minimal number of access policies and levels of access. By using these techniques, you spend less time assigning access to users and more time on developing in {{site.data.keyword.cloud_notm}} while ensuring that you don't provide too much access to users who don't need it.

Access groups are a useful tool for assigning access to a group of users and service IDs that all need the same access. By using access groups, you can streamline access management by assigning the minimal number of access policies to groups of users. As an example, if you have five users that you want to manage all of the billing and account management-related tasks for the enterprise, you can add them to an `Administrators` access group in the enterprise account. In the access group, you can assign two policies: one with the administrator role on the Billing account management service and one with the administrator role on all account management services in the account. As users change job responsibilities or teams, you can add or remove users from the access group instead of adding or removing the same policies from the individual users. See [Assigning enterprise access](/docs/enterprise-management?topic=enterprise-management-assign-access-enterprise) for more information.

For more information about centrally managing IAM access across your organization, see [Best practices for assigning access](/docs/enterprise-management?topic=enterprise-management-access-enterprises).

## Working with resources in an enterprise
{: #child-resources-enterprise}

Create resources only in child accounts that you import or create within the enterprise. Although it's possible to create resources within the enterprise account, it's not a best practice for the following reasons:

- The enterprise account is always a direct child of the enterprise and can't be moved, so you won't have the flexibility to change how usage is reported for the resources.
- The enterprise account contains the users and access for managing the enterprise and its billing, so only users with those responsibilities should be added to the account.

Users within each account in the enterprise can create, use, and collaborate on resources just as you can in a stand-alone account. For details, see [Managing resources](/docs/account?topic=account-manage_resource). Enterprise users can't directly work with resources within child accounts, but they can monitor the resource types and plans that are used in each account by viewing their usage. For more information, see [Viewing usage in an enterprise](/docs/enterprise-management?topic=enterprise-management-enterprise-usage).
