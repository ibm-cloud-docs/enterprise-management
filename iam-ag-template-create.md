---

copyright:
  years: 2023, 2024
lastupdated: "2024-11-22"

keywords: enterprise, enterprise account, multiple accounts, assign access, enterprise access, templates, enterprise managed, access, access group, migrate version, upgrade version, new version

subcollection: enterprise-management

---

{{site.data.keyword.attribute-definition-list}}

# Creating enterprise-managed access group templates
{: #ag-template-create}

In an enterprise where you have many child accounts, it can be time-consuming and error-prone to manually configure access groups for each account. Use enterprise-managed access group templates to save time and ensure consistency across all accounts.
{: shortdesc}

When an enterprise administrator assigns an access group template to child accounts, an enterprise-managed access group is created in each account. The associated attributes that you add to the template, like policies, members, or dynamic rules, are included.

## Members
{: #ag-enterprise-members}

When creating an access group template in the enterprise account, along with the set of associated access policies that grant permissions to the members of that group, you can include enterprise users and service IDs. Users that you add the access group template must be invited to the child accounts where the template is assigned to gain access. Then, the users are automatically added to the access groups in the target accounts where you assign the template.

Set up dynamic rules in an access group template to automatically add federated users in child accounts to enterprise-managed access groups based on specific identity attributes.
{: note}

By default, access group administrators in child accounts can't add members to the enterprise-managed access group in their account. To enable this capability, the enterprise account administrator must set this behavior in the access group template by using an action control. When enabled, this action control allows access group administrators to add members to the group in their account, even if those members aren't defined in the access group template. For more information, see [Action controls](/docs/enterprise-management?topic=enterprise-management-access-enterprises&interface=ui#action-controls) for members.

## Before you begin
{: #before-you-ag-template}

- To learn about how enterprise-manged IAM templates make your enterprise more secure, see [How enterprise-managed IAM access works](/docs/enterprise-management?topic=enterprise-management-access-enterprises&interface=ui#how-enterprise-iam).

- You must be a member of the enterprise account to create and assign enterprise-managed IAM templates.

- To create an enterprise-managed IAM template, make sure you're assigned the following access:
   * A policy with the Template Administrator role on All IAM Account Management services

- To assign an enterprise-managed IAM template to child accounts, make sure you're assigned the following access:
   * A policy with the Template Assignment Administrator role on All IAM Account Management services
   * A policy with at least the Viewer role on the Enterprise service

    By default, no users have the roles Template Administrator or Template Assignment Administrator, including the account owner.
    {: note}

- New and existing accounts in your enterprise must opt-in to enterprise-managed IAM. For more information, see [Opting in to enterprise-managed IAM](/docs/enterprise-management?topic=enterprise-management-enterprise-managed-opt-in).


## Creating an access group template
{: #create-ag-template}
{: ui}

Consider using access group templates when you have many child accounts, common access requirements across accounts, or strict security requirements.

To create an access group template, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Click **Create**.
1. Enter a name and description for the access group template that describes its purpose for enterprise users.
1. Enter a name and description for the enterprise-managed access group that describes its purpose for child account users. Use a unique access group name that doesn't conflict with the existing access groups in any child accounts.

   An error occurs when you assign the template if an account contains a conflicting access group name.
   {: note}

1. Click **Create**.

### (Optional) Add members
{: #add-members-template}
{: ui}

Enterprise members that you add to a template must be present in both the enterprise account and the child account. If an enterprise user is not yet a member of a child account that you assign a template to, add them to the child account.

Access group administrators in child accounts can add members to the access group in their account when you enable the **Add members** action control. This way, you can delegate managing membership to the access group administrators in child accounts.
{: tip}

To add enterprise members to the access group template, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select your access group template.
1. Click **Members > Add**.
1. Select the users that need access.
1. Click **Add**.
1. Click **Service IDs > Add** to add service IDs.
1. Select the service IDs that need the access in child accounts.

   Teams that use a script might add service IDs to help automate account setup.
   {: tip}

#### Action controls
{: #members-action-controls}
{: ui}

By default, access group administrators in child accounts can't add or remove members from enterprise-managed access groups in their account. You might want to allow them to add members so they can include members of their account that you can't add to a template as an enterprise user. Access group administrators can always remove members that they add when someone in the access group leaves the organization.

To change the default behavior, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select your access group template.
1. Click **Members**.
- Set the action control for **Add members** to **Yes** to allow access group administrators to add members to the enterprise-managed access group in their account. An access group administrator can remove any member that they add.
- Set the action control for **Remove members** to **Yes** to allow access group administrators to remove members from the enterprise-managed access group in their account that are added by the enterprise. This action control doesn't affect members that the access group administrator adds to the group.


### (Optional) Add dynamic rules
{: #add-dynamic-template}
{: ui}

You can create dynamic rules to automatically add federated users in child accounts to enterprise-managed access groups based on specific identity attributes. Set up conditions that must match the data that is configured within the identity provider (IdP) and passed in with a user's federated ID during login. Before you add dynamic rules, you must [Enable authentication from an external identity provider](/docs/account?topic=account-idp-integration).

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select your access group template.
1. Click **Dynamic rules > Add**.
1. Give the dynamic rule a name that describes what kind of users the rule adds to the access group.
1. Select **Users federated by IBMid** or **Users federated by {{site.data.keyword.appid_long}}** as the authentication method and input the identity prodiver (IdP).
1. Add conditions based on your IdP data to define which federated users are added to the group.
   1.  By clicking **Add a condition**, you can define multiple conditions. Federated users must meet all the conditions to gain membership in the access group. For more information about the fields that are used to create conditions, see [IAM condition properties](/docs/account?topic=account-iam-condition-properties).
1. Set the session duration in hours.

    Access group membership is revoked after this time period expires. Users must log back in to refresh their access group membership.
    {: note}

#### Action controls
{: #dynamic-rules-action-controls}
{: ui}

By default, access group administrators can't add, remove, or update dynamic rules for an enterprise-managed access group.

To change the default behavior for adding rules, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select your access group template.
1. Click **Dynamic rules**.
   - Set the action control for **Add dynamic rules** to **Yes** to allow access group administrators to add dynamic rules to the enterprise-managed access group in their account. An access group administrator can remove or update any dynamic rule that they add.


To change the default behavior for removing and updating enterprise-managed rules, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select your access group template.
1. Click **Dynamic rules**.
   - Set the action control for **Remove dynamic rules** to **Yes** to allow access group administrators to remove dynamic rules from the enterprise-managed access group in their account that are added by the enterprise. This action control doesn't affect dynamic rules that the access group administrator adds to the group.
   - Set the action control for **Update dynamic rules** to **Yes** to allow access group administrators to update dynamic rules for the enterprise-managed access group in their account that are added by the enterprise. This action control doesn't affect dynamic rules that access group administrators in child accounts add to the group.
1. Configure action controls for specific dynamic rules.
   1. Click the dynamic rule.
      - Set the action control for **Remove dynamic rule** to **Yes** to allow access group administrators in child accounts to remove this specific dynamic rule.
      - Set the action control for **Update dynamic rule** to **Yes** to allow access group administrators in child accounts to update this specific dynamic rule.
   1. Click **Save**.

### (Optional) Add access policies
{: #add-access-ag-template}
{: ui}

Access policies grant access in child accounts to the members of your enterprise-managed access group.

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select your access group template.
1. Click **Access > Add**.
1. Select an existing policy template and click **Add**.
1. Or, create a new policy template by clicking **Create**.
    1. Name and describe the policy that you want to assign.

    You create a policy template with every policy that you configure for an access group template. You can reference a policy template to assign access in other enterprise IAM templates.
    {: note}

    1. Select a service or group of services. Then, click **Next**.
    1. Select any combination of roles to define the scope of access, and click **Next**.
    1. (Optional) Add conditions to specify when you want the policy to grant access.
1. Click **Add**.

#### Remove access policies
{: #remove-access-ag-template}

You can remove policies before a template is committed and assigned.

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select your access group template.
1. Click **Access**
1. Click the actions icon on the policy that you want to remove.
1. Click **Remove**.

#### Action controls
{: #access-ag-action-controls}
{: ui}

By default, access group administrators in child accounts can't add access policies to an enterprise-managed access group. To allow access group administrators to add policies, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select your access group template.
1. Click **Access**
1. Set the action control for **Add policies** to **Yes** to allow access group administrators in child accounts to add access policies to the enterprise-managed access group in their account.

Any policy that access group administrators add to the enterprise-managed access group in their account, they can also remove and update.
{: note}



## Updating template details
{: #update-ag-template-name}
{: ui}

You can update the template name, access group name, and descriptions at any time before you commit the template. To update template details, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select the access group template that you want to update.
1. Click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit") in the Details section.
1. Make necessary updates to the template name, access group name, and descriptions.
1. Click **Save**.

If you need to make updates after you commit the template, create a new version.
{: tip}

## Reviewing your access group template
{: #review-ag-template}
{: ui}

Review the access group template and commit it so that no further changes can be made to the version. This way, the Template Assignment Administrator can be sure that they assign the version only when you have confirmed that it's ready.

1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select the access group template that you want to review.
1. Click **Review**.
1. Verify that the access group template is configured correctly.
1. Click the checkbox to confirm that you can't make changes to the version.
1. Click **Commit**.

## Assigning an access group template to child accounts
{: #assign-ag-template}
{: ui}

Assign the access group template to child accounts in your enterprise.

You can't assign an IAM template to the enteprise account, only child accounts.
{: note}

1. Click **Assign accounts**.
1. Select the accounts and account groups that you want to assign the access group template to.

   In each of the child accounts that you assign the template to, you create an enterprise-managed access group. Users in the child account can determine that an access group comes from an enterprise-managed IAM template by the [enterprise-managed]{: tag-cyan} tag on the group.

1. Click **Assign**.

If an assignment fails, click **Retry**.
{: tip}

## Creating a new version
{: #new-version-ag-template}
{: ui}

If you want to make changes to an access group template that's committed or assigned, create a new version. You can create a new version based on your latest version, or a different version that you select.

To create a new version of an access group template, complete the following steps:
1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select your access group template.
1. Click the **New version** icon ![New version icon](../icons/new-version.svg "New version").
1. Select the version that you want as the basis for your new version.
1. Enter a new template name and description or keep the ones that you're already using.

    Entering a new template name updates the template name for this version and all previous versions. The template description is stored speparately for each version.
    {: note}

1. Enter a new access group name and description or keep the ones you're already using.

    Entering a new access group name replaces the previous access group name shown in child accounts after you assign the new version.
    {: note}

1. Select the objects that you want to carry over to your new version.
   1. (Optional) Select **Members**.
   1. (Optional) Select **Dynamic rules**.
   1. (Optional) Select **Access**.
1. Click **Create**.
1. Make any other adjustments to the configuration.
1. Click **Review** and commit the new version. For more information, see [Reviewing your access group template](/docs/enterprise-management?topic=enterprise-management-ag-template-create&interface=ui#review-ag-template).

To assign a new version of an access group template, complete the following steps:
1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Click the **Table expand** icon ![Table expand icon](../icons/table-expand.svg "Table expand") on the template that you want to work with.
1. Select the version that's currently assigned to child accounts.
1. Click **Assignments**.
1. Click **Update** on the account or account group assignment where you want to assign a different version.
1. Click **Select a version**.
   1. Select the version that you want to replace the current version.
1. Click **Update**.
1. Repeat these steps for each account or account group where you want to assign a different version.

The new template version that you assign replaces the old version. Learn more about [Assigning a new version](/docs/enterprise-management?topic=enterprise-management-working-with-versions#new-version).
{: note}



## Removing an assignment
{: #remove-assignment-ag}
{: ui}

You can remove a template assignment from one or more accounts where the template is assigned. You might want to do so if the template isn't working as intended. When you remove a template assignment from an account, by default the previous version of the template is reinstated. If the assignment you remove is for the first or only version of a template, the access group in the child account is removed.

To remove an assignment, complete the following steps:
1. Go to **Manage > Access (IAM) > Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Select your access group template.
1. Click **Update assignments**.
   1. To remove an assignment from one or a few accounts, deselect the accounts where you want to remove the template assignment.
   1. To remove an assignment from all accounts where the template is assigned, click **Unassign all**.

## Creating an access group template by using the API
{: #create-ag-template-api}
{: api}

Consider using access group templates when you have a large number of child accounts, common access requirements across accounts, strict security requirements, or need to make changes to access policies.

You can programmatically create an access group template by calling the [IAM Access Groups API](/apidocs/iam-access-groups#create-template) as shown in the following sample request. The example creates an access group template for managers who need administrator access to all IAM account management services in child accounts so that they can manage access:

```bash
{
    curl -X POST --location
    --header "Authorization: Bearer {iam_token}"
    --header "Accept: application/json"   --header "Content-Type: application/json"
    --data "name": "IAM Admin Group template",
    "description": "This access group template allows admin access to all IAM platform services in the account.",
    "account_id": "06a2e9d0614447e295824de8c8df7b4f",
    "access_group": {
        "name": "IAM Admin Group",
        "description": "This enterprise-managed access group allows admin access to all IAM platform services in the account. Managers are dynamically added.",
        "members": {
            "users": [
                "IBMid-1234",
                "IBMid-2345"
            ],
            "services": [
                "iam-ServiceId-123",
                "iam-ServiceId-234"
            ],
            "action_controls": {
                "add": "true",
                "remove": "false"
            }
        },
        "assertions": {
            "rules": [
                {
                    "name": "Manager group rule",
                    "expiration": 12,
                    "realm_name": "https://idp.example.org/SAML2",
                    "conditions": [
                        {
                            "claim": "isManager",
                            "operator": "EQUALS",
                            "value": "true"
                        }
                    ],
                    "action_controls": {
                        "remove": "true",
                        "update": "false"
                    }
                }
            ],
            "action_controls": {
                "add": "false"
            }
        },
        "action_controls": {
            "access": {
                "add": true
            }
        }
    },
    "policy_template_references": [
        {
            "id": "policyTemplateId-123",
            "version": "1"
        },
        {
            "id": "policyTemplateId-234",
            "version": "1"
        }
    ],
    "externals": {
        "profile_template_ids": [
            "profileTemplateId-123",
            "profileTemplateId-234"
        ]
    }
}

```
{: curl}
{: codeblock}

### (Optional) Add members
{: #add-members-template-api}
{: api}

In the previous example, two enterprise users and two service IDs are added to the access group template by specifying their IBMids.

Enterprise members that you add to a template must be present in both the enterprise account and the child accounts that you want to assign the template to. If a user is not already a member of a child account that you assign a template to, you can add them to that child account.

#### Action controls
{: #members-action-controls-api}
{: api}

By default, access group administrators in child accounts can't add or remove members from enterprise-managed access groups in their account. You might want to allow them to add members so they can include members of their account that you can't add to a template as an enterprise user. Access group administrators can always remove members that they add when someone in the access group leaves the organization.

In the previous example, the `action_controls` allow access group administrators in child accounts to add members from their own account because `add` is set to `true` and restricts removing enterprise members because `remove` is set to `false`.

### (Optional) Add dynamic rules
{: #add-dynamic-template-api}
{: api}

You can create dynamic rules to automatically add federated users in child accounts to enterprise-managed access groups based on specific identity attributes. Set up conditions that must be matched by the data that is configured within the identity provider (IdP) and passed in with a user's federated ID during login. Before you add dynamic rules, you must [Enable authentication from an external identity provider](/docs/account?topic=account-idp-integration).

In the previous example, managers are dynamically added to the group by the `rules` specified in the `assertions` section. The session duration is set to `12` hours for dynamically added users. Access group membership is revoked after this time period expires. Users must log back in to refresh their access group membership.

#### Action controls
{: #dynamic-rules-action-controls-api}
{: api}

By default, access group administrators can't add, remove, or update dynamic rules for an enterprise-managed access group. There are two levels of action controls for dynamic rule:
- Action controls for each specific rule that determine if access group administrators can remove or update a specific dynamic rule
- Action controls that determine if access group administrators can add, remove, or update dynamic rules for the acces group

If both levels are configured, the inner level action controls for specific dynamic rule take precedence.

In the previous example, the inner level action controls set `remove` to `true`, which allow access group administrators to remove the rule. `update` is set to `false`, so access group administrators can't update the rule. The outer leel action control `add` is set to `false`, so access group administrators can't add any new dynamic rules.

### (Optional) Add access policies
{: #add-access-ag-template-api}
{: api}

Access policies grant access to the members of your enterprise-managed access group in child accounts. In the previous example, existing policy templates assign access in the access group template by using `policy_template_references`.

#### Action controls
{: #access-ag-action-controls-api}
{: api}

By default, access group administrators in child accounts can't add access policies to an enterprise-managed access group. In the previous example, the `access` action control for `add` is set to `true`, so child account administrators can add policies to the group in their account.

## Updating access group templates by using the API
{: #update-ag-template-api}
{: api}

You can update an access group template at any time before a template is committed.

To update an access group template, call the [IAM Policy Management API](/apidocs/iam-policy-management#delete-policy-assignment) as shown in the following sample request:

```bash
curl -X PUT --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" --header "If-Match: {if_match}" --header "Content-Type: application/json" --data '{ "name": "IAM Admin Group template 2", "description": "This access group template allows admin access to all IAM platform services in the account.", "group": { "name": "IAM Admin Group 8", "description": "This access group template allows admin access to all IAM platform services in the account.", "members": { "users": [ "IBMid-665000T8WY" ], "services": [ "iam-ServiceId-e371b0e5-1c80-48e3-bf12-c6a8ef2b1a11" ], "action_controls": { "add": true, "remove": false } }, "assertions": { "rules": [ { "name": "Manager group rule", "expiration": 12, "realm_name": "https://idp.example.org/SAML2", "conditions": [ { "claim": "blueGroup", "operator": "CONTAINS", "value": "test-bluegroup-saml" } ], "action_controls": { "remove": false, "update": false } } ], "action_controls": { "add": false } }, "action_controls": { "access": { "add": false } } }, "policy_template_references": [ { "id": "policyTemplateId-123", "version": "1" }, { "id": "policyTemplateId-234", "version": "1" } ] }' "{base_url}/v1/group_templates/{template_id}/versions/{version_num}"
```
{: curl}
{: codeblock}

## Reviewing and committing your access group template by using the API
{: #review-ag-template-api}
{: api}

Review the access group template and commit it so that no further changes can be made to the version. This way, the Template Assignment Administrator can be sure that they assign the version only when you have confirmed that it's ready.

1. List the access group templates in your enterprise account and note the `id` of the template you want to review and commit.

   ```bash
   curl -X GET --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" "{base_url}/v1/group_templates?account_id=accountID-123&limit=50&offset=0&verbose=false"
   ```
   {: codeblock}
   {: curl}

1. Get the template version and review the response.

   ```bash
   curl -X GET --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" "{base_url}/v1/group_templates/{template_id}/versions/{version_num}"
   ```
   {: codeblock}
   {: curl}

2. Commit the template version.

   ```bash
   curl -X POST --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" --header "If-Match: {if_match}" "{base_url}/v1/group_templates/{template_id}/versions/{version_num}/commit"
   ```
   {: codeblock}
   {: curl}

## Assigning an access group template to child accounts by using the API
{: #assign-ag-template-api}
{: api}

Assign the access group template to child accounts in your enterprise.

You can't assign an IAM template to the enteprise account, only child accounts.
{: note}

1. List the access group templates in your enterprise account and note the the `id` of the template you want to assign to child accounts.

   ```bash
   curl -X GET --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" "{base_url}/v1/group_templates?account_id=accountID-123&limit=50&offset=0&verbose=false"
   ```
   {: codeblock}
   {: curl}

1. Assign the access group template to an `Account` or `AccountGroup`.

   ```bash
   curl -X POST --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" --header "Content-Type: application/json" --data '{ "template_id": "AccessGroupTemplateId-4be4", "template_version": "1", "target_type": "AccountGroup", "target": "0a45594d0f-123" }' "{base_url}/v1/group_assignments"
   ```
   {: codeblock}
   {: curl}

## Creating a new version by using the API
{: #new-version-ag-template-api}
{: api}

If you want to make changes to an access group template that's committed or assigned, create a new version. Entering a new template name updates the template name for this version and all previous versions.

1. List the access group templates in your enterprise account and note the the `id` of the template for which you want to create a new version.

   ```bash
   curl -X GET --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" "{base_url}/v1/group_templates?account_id=accountID-123&limit=50&offset=0&verbose=false"
   ```
   {: codeblock}
   {: curl}

1. Create a new version and include any updates that you want to make.

   ```bash
   curl -X POST --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" --header "Content-Type: application/json" --data '{ "name": "IAM Admin Group template 2", "description": "This access group template allows admin access to all IAM platform services in the account.", "group": { "name": "IAM Admin Group 8", "description": "This access group template allows admin access to all IAM platform services in the account.", "members": { "users": [ "IBMid-123", "IBMid-234" ], "services": [ "iam-ServiceId-345" ], "action_controls": { "add": true, "remove": false } }, "assertions": { "rules": [ { "name": "Manager group rule", "expiration": 12, "realm_name": "https://idp.example.org/SAML2", "conditions": [ { "claim": "blueGroup", "operator": "CONTAINS", "value": "test-bluegroup-saml" } ], "guardrails": { "remove": false, "update": false } } ], "action_controls": { "add": false } }, "action_controls": { "access": { "add": false } } }, "policy_template_references": [ { "id": "policyTemplateId-123", "version": "1" }, { "id": "policyTemplateId-234", "version": "1" } ] }' "{base_url}/v1/group_templates/{template_id}/versions"
   ```
   {: codeblock}
   {: curl}

Once you've created and configured a new version of your access group template, review it and assign it to child accounts. You can assign a new version to child accounts that contain a previous version of the access group template to seamlessly update an assignment. For more information, see [Assigning an access group template to child accounts by using the API](/docs/enterprise-management?topic=enterprise-management-ag-template-create&interface=api#assign-ag-template-api).

## Removing an assignment by using the API
{: #remove-ag-assignment-api}
{: api}

You can remove a template assignment from an account or account group where the template is assigned. You might want to do so if the template isn't working as intended or isn't needed anymore. When you remove a template assignment from an account, by default the previous version of the template is reinstated if one exists. If the assignment you remove is for the first or only version of a template, the enterprise-managed access group in the child accounts are removed.

To remove an assignment, complete the following steps:

1. List the assignments and note the `AccessGroupAssignmentId` in the response for the assignment that you want to remove.

   ```bash
    curl -X GET --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" "{base_url}/v1/group_assignments?account_id=accountID-123&limit=50&offset=0"
   ```
   {: curl}
   {: codeblock}

1. Remove the assignment.

   ```bash
   curl -X DELETE --location --header "Authorization: Bearer {iam_token}" "{base_url}/v1/group_assignments/{assignment_id}"
   ```
   {: curl}
   {: codeblock}

## Deleting a version by using the API
{: #delete-ag-template-version}
{: api}

Before you can delete an access group template version, you must remove all assignments for that version of the template. Delete a specific version by completing the following steps:

1. List the access group templates in your enteprise account and note the `AccessGroupTemplateId` ID and version in the response for the template version that you want to delete.

   ```bash
    curl -X GET --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" "{base_url}/v1/group_templates?account_id=accountID-123&limit=50&offset=0&verbose=true"
   ```
   {: curl}
   {: codeblock}

1. Delete the version.

   ```bash
   curl -X DELETE --location --header "Authorization: Bearer {iam_token}" "{base_url}/v1/group_templates/{template_id}/versions/{version_num}"
   ```
   {: curl}
   {: codeblock}

## Creating an access group template by using the CLI
{: #create-ag-template-cli}
{: cli}

Consider using access group templates when you have a large number of child accounts, common access requirements across accounts, strict security requirements, or need to make changes to access policies in your enterprise.

You can create an access group template by completing the following steps:

1. Create a JSON file with your access group template definition. For more information about the attributes you can use, see the [IAM Access Groups API](/apidocs/iam-access-groups#create-template). The following example creates an access group template for managers who need administrator access to all IAM account management services in child accounts so that they can manage access:

    ```bash
    {
        "name": "IAM Admin Group template",
        "description": "This access group template allows admin access to all IAM platform services in the account.",
        "account_id": "06a2e9d0614447e295824de8c8df7b4f",
        "access_group": {
            "name": "IAM Admin Group",
            "description": "This enterprise-managed access group allows admin access to all IAM platform services in the account. Managers are dynamically added.",
            "members": {
                "users": [
                    "IBMid-1234",
                    "IBMid-2345"
                ],
                "services": [
                    "iam-ServiceId-123",
                    "iam-ServiceId-234"
                ],
                "action_controls": {
                    "add": "true",
                    "remove": "false"
                }
            },
            "assertions": {
                "rules": [
                    {
                        "name": "Manager group rule",
                        "expiration": 12,
                        "realm_name": "https://idp.example.org/SAML2",
                        "conditions": [
                            {
                                "claim": "isManager",
                                "operator": "EQUALS",
                                "value": "true"
                            }
                        ],
                        "action_controls": {
                            "remove": "true",
                            "update": "false"
                        }
                    }
                ],
                "action_controls": {
                    "add": "false"
                }
            },
            "action_controls": {
                "access": {
                    "add": true
                }
            }
        },
        "policy_template_references": [
            {
                "id": "policyTemplateId-123",
                "version": "1"
            },
            {
                "id": "policyTemplateId-234",
                "version": "1"
            }
        ],
        "externals": {
            "profile_template_ids": [
                "profileTemplateId-123",
                "profileTemplateId-234"
            ]
        }
    }

    ```
    {: curl}
    {: codeblock}

1.  Use the [access-group-template-create](/clidocs/iam-access-groups#create-template) method as shown in the following sample request:

    ```bash
    ibmcloud iam access-group-template-create --output JSON --file /path/to/access_group_template.json
    ```
    {: curl}
    {: codeblock}

### (Optional) Add members
{: #add-members-template-cli}
{: cli}

In the previous example, two enterprise users and two service IDs are added to the access group template by specifying their IBMids.

Enterprise members that you add to a template must be present in both the enterprise account and the child accounts that you want to assign the template to. If a user is not already a member of a child account that you assign a template to, you can add them to that child account.

#### Action controls
{: #members-action-controls-cli}
{: cli}

By default, access group administrators in child accounts can't add or remove members from enterprise-managed access groups in their account. You might want to allow them to add members so they can include members of their account that you can't add to a template as an enterprise user. Access group administrators can always remove members that they add when someone in the access group leaves the organization.

In the previous example, the `action_controls` allow access group administrators in child accounts to add members from their own account because `add` is set to `true` and restricts removing enterprise members because `remove` is set to `false`.

### (Optional) Add dynamic rules
{: #add-dynamic-template-cli}
{: cli}

You can create dynamic rules to automatically add federated users in child accounts to enterprise-managed access groups based on specific identity attributes. Set up conditions that must be matched by the data that is configured within the identity provider (IdP) and passed in with a user's federated ID during login. Before you add dynamic rules, you must [Enable authentication from an external identity provider](/docs/account?topic=account-idp-integration).

In the previous example, managers are dynamically added to the group by the `rules` specified in the `assertions` section. The session duration is set to `12` hours for dynamically added users. Access group membership is revoked after this time period expires. Users must log back in to refresh their access group membership.

#### Action controls
{: #dynamic-rules-action-controls-cli}
{: cli}

By default, access group administrators can't add, remove, or update dynamic rules for an enterprise-managed access group. There are two levels of action controls for dynamic rule:
- Action controls for each specific rule that determine if access group administrators can remove or update a specific dynamic rule
- Action controls that determine if access group administrators can add, remove, or update dynamic rules for the acces group

If both levels are configured, the inner level action controls for specific dynamic rule take precedence.

In the previous example, the inner level action controls set `remove` to `true`, which allow access group administrators to remove the rule. `update` is set to `false`, so access group administrators can't update the rule. The outer leel action control `add` is set to `false`, so access group administrators can't add any new dynamic rules.

### (Optional) Add access policies
{: #add-access-ag-template-cli}
{: cli}

Access policies grant access to the members of your enterprise-managed access group in child accounts. In the previous example, existing policy templates assign access in the access group template by using `policy_template_references`.

#### Action controls
{: #access-ag-action-controls-cli}
{: cli}

By default, access group administrators in child accounts can't add access policies to an enterprise-managed access group. In the previous example, the `access` action control for `add` is set to `true`, so child account administrators can add policies to the group in their account.

## Updating access group templates by using the CLI
{: #remove-access-ag-template-cli}
{: cli}

You can update an access group template at any time before a template is committed.

To update an access group template, complete the following steps:

1. Update your JSON file with the new access group template definition. For more information about the attributes that you can use in your JSON file, see the [IAM Access Groups API](/apidocs/iam-access-groups#create-template).
1. Use the `access-group-template-version-update` method as shown in the following sample request:

    ```bash
    ibmcloud iam access-group-template-version-update example-template-name 1 --file /path/to/access_group_template.json
    ```
    {: codeblock}
    {: curl}

    This example request updates version `1` of a template `example-template-name`.

## Reviewing and committing your access group template by using the CLI
{: #review-ag-template-cli}
{: cli}

Review the access group template and commit it so that no further changes can be made to the version. This way, the Template Assignment Administrator can be sure that they assign the version only when you have confirmed that it's ready.

1. List the access group templates in your enterprise account and note the `id` of the template that you want to review and commit.

   ```bash
    ibmcloud iam access-group-templates
   ```
   {: codeblock}
   {: curl}

1. Get the template version and review the response.

    ```bash
    ibmcloud iam access-group-template example-template-name 1
    ```
    {: codeblock}

2. Commit the template version.

    ```bash
    ibmcloud iam access-group-template-version-commit example-template-name 1
    ```
    {: codeblock}

## Assigning an access group template to child accounts by using the CLI
{: #assign-ag-template-cli}
{: cli}

Assign the access group template to child accounts in your enterprise.

You can't assign an IAM template to the enteprise account, only child accounts.
{: note}

1. List the access group templates in your enterprise account and note the the `id` of the template you want to assign to child accounts.

   ```bash
   ibmcloud iam access-group-templates
   ```
   {: codeblock}
   {: curl}

1. Assign the access group template to an `Account` or `AccountGroup`.

   ```bash
   ibmcloud iam access-group-assignment-create example-template-name 1 --target-type Account --target example-account-id
   ```
   {: codeblock}
   {: curl}

## Creating a new version by using the CLI
{: #new-version-ag-template-cli}
{: cli}

If you want to make changes to an access group template that's committed or assigned, create a new version. Entering a new template name updates the template name for this version and all previous versions.

1. List the access group templates in your enterprise account and note the the `id` of the template for which you want to create a new version.

   ```bash
   ibmcloud iam access-group-templates
   ```
   {: codeblock}
   {: curl}

1. Create a JSON file that includes any updates that you want to make. For more information about the attributes that you can use in your JSON file, see the [IAM Access Groups API](/apidocs/iam-access-groups#create-template).

1. Create a new version by using the `access-group-template-version-create` method as shown in the following sample request:

   ```bash
   ibmcloud iam access-group-template-version-create example-template-id 1
   ```
   {: codeblock}
   {: curl}

Once you've created and configured a new version of your access group template, commit it and assign it to child accounts. You can assign a new version to child accounts that contain a previous version of the access group template. The new template version replaces the old version in that case. For more information, see [Assigning an access group template to child accounts by using the CLI](/docs/enterprise-management?topic=enterprise-management-ag-template-create&interface=cli#assign-ag-template-cli).
