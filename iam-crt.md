---

copyright:
  years: 2025
lastupdated: "2025-12-12"

keywords: enterprise, enterprise account, multiple accounts, assign access, enterprise access, templates, enterprise managed, access, settings, migrate version, upgrade version, new version, enterprise role template

subcollection: enterprise-management

---

{{site.data.keyword.attribute-definition-list}}

# Creating enterprise role templates
{: #crt-roletemplate-create}

In large enterprises with multiple child accounts, manually configuring access restrictions and permissions across accounts can be complex and time-consuming. To help ensure consistent security and compliance, enterprise admins can centrally create and assign custom roles to subaccounts, enforcing the principle of least privilege. This capability simplifies role management and helps maintain uniform governance across your organization’s accounts.
{: shortdesc}

## Before you begin
{: #before-you-begin-ole-template}

- To learn about how enterprise-manged IAM templates make your enterprise more secure, see [How enterprise-managed IAM access works](/docs/enterprise-management?topic=enterprise-management-access-enterprises&interface=ui#how-enterprise-iam).

- Be a member of the enterprise account to create and assign enterprise-managed IAM templates.

- To create, update, and delete an enterprise-managed IAM template, make sure that you are assigned with the following access:
    * A policy with the template administrator role on All IAM account management services.

- To assign an enterprise-managed IAM template to child accounts, make sure that you are assigned with the following access:
    * A policy with the template assignment administrator role on All IAM account management services.
    * A policy with at least the Viewer role on the Enterprise service.

- To read an enterprise-managed IAM template or the template assignment, make sure you're assigned with the following access:
    * A policy with the template administrator role on All IAM account management services.
    * A policy with the template assignment administrator role on All IAM account management services.

   By default, no users have the roles of template administrator or template assignment administrator, including the account owner.
   {: note}

- To create and assign enterprise role templates, new and existing accounts in your enterprise must opt-in to enterprise-managed IAM. For more information, see [Opting in to enterprise-managed IAM](/docs/enterprise-management?topic=enterprise-management-enterprise-managed-opt-in).

## Creating an enterprise role template
{: #create-crt-standalone}

You can create enterprise role templates when you have many child accounts that require the same service restrictions.

To create an enterprise role template, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Access (IAM) > Enterprise > Templates**, and select **Roles**.
1. Click **Create**.
1. On the **Create role template** page, enter the required details in the **Enterprise account** and **Child account** sections and click **Create**.
1. On the newly created template page, click **Configuration** to configure the role template by completing the following steps:
    1. In the **Service** section, select a service to view available actions.
    1. Select an action from the list by checking the appropriate boxes. Make sure at least one of the selected actions is service-based which means the type must be **Service**.
    1. Set the toggle to **View selected only** to review the actions that are added.
    1. Click **Save** to update your template.
1. Click **Review** on the upper right of the template page.
1. On the **Review and commit** page, select the confirmation to commit the template and click **commit**. Until you commit, the template is the `Draft` state. After you commit, the template will be in the `Committed` state.

You can assign enterprise role templates to child accounts and account groups only after you commit.
{: note}

## Assigning an enterprise role template to child accounts
{: #assign-crt}

You can assign enterprise role templates to child accounts and account groups to restrict certain actions. To assign a role template, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Access (IAM) > Enterprise > Templates**, and select **Roles**.
1. Select any enterprise role template.
1. Click **Assign accounts** on the upper right of the template page.
1. Select the accounts and account groups for which you like to assign the role template.

   If you select an account group, the template gets assigned to all current and future child accounts of that group.
   {: note}

1. Click **Assign accounts** to assign the enterprise role template to the specified accounts or account groups.

## Updating an enterprise role template
{: #update-crt}

To update an enterprise role template, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Access (IAM) > Enterprise > Templates**, and select **Role**.
1. Select any enterprise role template.
1. Click **Assign accounts** to modify the assignments. You can change the specified accounts or account groups that are assigned to the template.

Users can also edit template details on the **Overview** and **Configuration** tabs.
{: note}

After you commit the enterprise role templates, you will not be able to edit them, but you can create another version of the template.
{: note}

## Creating a new version
{: #new-version-act-create-ui}

To create a new version of the enterprise role template, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Access (IAM) > Enterprise > Templates**, and select **Role**.
1. Select any enterprise role template.
1. Click **Create new version** on the upper right of the template page.
1. On the **Create new version** page, enter the required details in the **Enterprise account** and **Child account** sections and click **Create**.

## Updating a version
{: #update-version}

To update an enterprise role template assignment, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Access (IAM) > Enterprise > Templates**, and select **Role**.
1. Select any enterprise role template that has multiple committed versions.
1. Click **Assignments** tab, for a particular assignment, click **Update**.
1. Select the version and click **Update** to update the template version that is assigned to the child accounts.

## Unassigning an enterprise role template
{: #unassign-role-template}

To remove an enterprise role template assignment, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Access (IAM) > Templates**, and select **Role**.
1. Select any enterprise role template.
1. Click the **Actions** icon ![Actions](../icons/action-menu-icon.svg "Actions"), and click **Details** to view the assignment details.
1. On the **Assignment report** page, click **Unassign all**.
1. You can also remove a template assignment from the **Actions** icon ![Actions](../icons/action-menu-icon.svg "Actions") icon, and select **Remove**.
1. Click **Remove** to confirm the removal of template assignment.

## Deleting an enterprise role template
{: #delete-crtt-version}

To delete a version of an enterprise role template or delete an enterprise role template, you must unassign all the assignments for the template.
{: note}

To delete an enterprise role template or enterprise role template version, follow these steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Access (IAM) > Enterprise > Templates**, and select **Role**.
1. For any particular role template or role template version, click the **Actions** icon ![Actions](../icons/action-menu-icon.svg "Actions") and select **Delete template** or **Delete version**.
1. If the template has any assignments, select the role template and remove all the associated assignments.
1. Click the **Delete** icon ![Delete](../icons/delete.svg "Delete") and click **Delete** to confirm the deletion of a template version.
