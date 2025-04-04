---

copyright:
  years: 2023, 2025
lastupdated: "2025-04-04"

keywords: enterprise, enterprise account, multiple accounts, enterprise access, templates, enterprise managed, versions, versioning. template version, migrate version, upgrade version, new version

subcollection: enterprise-management

---

{{site.data.keyword.attribute-definition-list}}

# Working with template versions
{: #working-with-versions}

As your organization builds out Identity and Access Management (IAM) best practices with enterprise-managed IAM templates, you might need to create new versions or reorganize your enterprise by moving accounts between account groups. Confidently manage versioning in your enterprise by reviewing the following information.

## Creating a new version
{: #create-new-version}

If you want to update an IAM template that's committed or assigned, create a new version. You can create a new version based on your latest version, or a different version that you select.

To create a new version of an IAM template, complete the following steps:
1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select the template type that you want to work with:
   1. Access groups
   1. Trusted profiles
   1. Settings
1. Select the specific template that you want to create a new version of.
1. Click the **New version** icon ![New version icon](../icons/new-version.svg "New version").
1. Select the version that you want as the basis for your new version.
1. Enter a new template name and description or keep the ones that you're already using.

    Entering a new template name updates the template name for this version and all previous versions. However, the template description can be unique for each version.
    {: note}

1. Enter a new name and description for the IAM resource or keep the ones you're already using.

    Entering a new name for the IAM resource replaces the name of the previous version that is shown in child accounts after you assign the new version.
    {: note}

1. Select the objects that you want to carry over to your new version.
1. Click **Create**.

For more information about creating a new version, see the documentation for [access group templates](/docs/enterprise-management?topic=enterprise-management-ag-template-create&interface=ui#new-version-ag-template), [trusted profile templates](/docs/enterprise-management?topic=enterprise-management-tp-template-create&interface=ui), and [settings templates](/docs/enterprise-management?topic=enterprise-management-settings-template-create&interface=ui).

## Assigning a new version
{: #new-version}

Assigning a new version of an IAM template to accounts where a previous version is assigned updates the IAM resources that the template creates in those accounts to match the new version. The old version becomes inactive in your assignment record and can become active again if you [move an account](/docs/enterprise-management?topic=enterprise-management-working-with-versions#move-account) within your enterprise. If the IAM template that you're replacing includes action controls that enable child account administrators to make changes to the IAM resource in their account, review the behavior of possible [scenarios](/docs/enterprise-management?topic=enterprise-management-working-with-versions#new-version-scenarios).

To assign a new version of an IAM template, complete the following steps:
1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select the template type that you want to work with:
   1. Access groups
   1. Trusted profiles
   1. Settings
1. Click the **Table expand** icon ![Table expand icon](../icons/table-expand.svg "Table expand") on the template that you want to work with.
1. Select the version that is assigned to child accounts.
1. Click **Assignments**.
1. Click **Update** on the account or account group assignment where you want to assign a different version.
1. Click **Select a version**.
   1. Select the version that you want to replace the current version.
1. Click **Update**.
1. Repeat these steps for each account or account group where you want to assign a different version.

### Assigning a new version scenarios
{: #new-version-scenarios}

Access group templates have action controls that might allow access group administrators in child accounts to make changes to the enterprise-managed access group in their account, like adding members or updating dynamic rules. In the case that an IAM administrator in a child account made changes to the initial version in their account, the following scenarios might occurr when you assign a new version.

Action controls are available for only access group templates.
{: note}

#### Handling attributes added by a child account
{: #replace-ac-allow}

Let's say that you've assigned `v1` of an access group template to `account-1`. The template includes action controls that enable access group administrators in the  child account to add members to the enterprise-managed group in their account. An access group administrator in `account-1` then adds members of their account to the enterprise-managed group. Next, you create `v2` with action controls that don't allow adding members to the enterprise-managed group in child accounts. When you try to assign `v2` to `account-1`, the assignment fails because the members added by the child account conflicts with the action control that disallows adding members.

If the new version of a template that you're assigning has action controls that are more strict than the current version, the assignment could fail. In that case, you must resolve the conflict to continue.
{: important}

To resolve the conflict, the enterprise administrator can contact the owner of the child account and ask them to remove the conflicting members of the enterprise-managed group. Or, assign a template that maintains the action control that allows adding members. This way, when you assign the new version, the members that the child account added remain in the enteprise-managed group.

#### Handling attributes deleted by a child account
{: #deleted-attributes}

Let's say that you that you've assigned `v1` of an access group template to `account-2`. The template includes two enterprise members and action controls that allow child account administrators to remove enterprise members from the enterprise-managed group in their account. An access group administrator in `account-2` then removes the enterprise members from the group in their account. Then, you create `v2` that maintains the same action controls and original enterprise members. You can assign `v2` and the deleted members are restored in the child account. Deleted members are also restored in the case that `v2` action controls disallow removing members.

Deleted attributes are restored by assigning a new version or reassigning the current version.
{: important}


## Superseeding a version
{: #template-superseded}

IAM templates that you assign at the account group level have priority over assignments that are made at the account level. For example, there are two assignments for `Admin template`: one at the account level and another at the account group level where the account group serves as the parent of the account. The assignment at the account group level takes precedence, regardless of the template version. This precedence is independent of the order in which you assign the template. The assignment at the account level is inactive in this scenario and can become active again if you [move an account](/docs/enterprise-management?topic=enterprise-management-working-with-versions#move-account) within your enterprise.

## Moving an account
{: #move-account}

Accounts in your enterprise might have a history of different enterprise-managed IAM template assignments. You can replace a template assignment by assigning a newer version or superseded an assignment by assigning a template at a higher level, such as the account group level. In these cases, the previous assignment of a template becomes inactive while the versions with higher-level assignments remain active.

You might want to remove inactive assignments before you move an account to avoid granting access unintentionally in the account.
1. To view a record of assignments, go to **Manage > Access (IAM) > Templates**, select your template and version, and go to **Assignments**.
1. Remove an assignment by clicking the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Delete**.

## Removing an assignment
{: #remove-assignment}

Removing a template assignment from an account deletes the assigned IAM resources in the target child account. If a previous assignment exisits, removing the assignment reinstates the previous assignment. When you remove a settings template assignment and no previous assignments exist, the settings that are configured at the account level are restored.
