---

copyright:
  years: 2025
lastupdated: "2025-10-14"

keywords: enterprise, enterprise account, multiple accounts, assign access, enterprise access, templates, enterprise managed, access, settings, migrate version, upgrade version, new version, action control template

subcollection: enterprise-management

---

{{site.data.keyword.attribute-definition-list}}

# Creating enterprise-managed action control templates
{: #act-template-create}

In an enterprise where you have many child accounts, it can be difficult to manually configure restrictions on child accounts to manage various settings for the Observability routers such as {{site.data.keyword.atracker_full}}, {{site.data.keyword.logs_routing_full}}, and {{site.data.keyword.metrics_router_full}}. Make sure that all accounts in your enterprise adhere to your organization's security requirements by using action control templates.
{: shortdesc}


As an enterprise IAM administrator, you can centrally restrict child account users from performing certain actions in the child accounts even if they have an access policy that grants them access.

You can assign only one action control template to an account or an account group. Create an action control template that applies to the most accounts and create a new one only for accounts that have special requirements. For example, you want to centrally disable deleting the auditing events for some or all child accounts within your enterprise.

You cannot delete or update the action controls created from templates. The only way to delete or update them is through remove or update action control assignment.
{: note}

## Before you begin
{: #before-you-actioncontrol-template}

- To learn about how enterprise-manged IAM templates make your enterprise more secure, see [How enterprise-managed IAM access works](/docs/enterprise-management?topic=enterprise-management-access-enterprises&interface=ui#how-enterprise-iam).

- Be a member of the enterprise account to create and assign enterprise-managed IAM templates.

- To create, update, and delete an enterprise-managed IAM template, make sure that you are assigned with the following access:
   * A policy with the Template Administrator role on All IAM Account Management services.

- To assign an enterprise-managed IAM template to child accounts, make sure that you are assigned with the following access:
   * A policy with the Template Assignment Administrator role on All IAM Account Management services
   * A policy with at least the Viewer role on the Enterprise service.

- To read an enterprise-managed IAM template or the template assignment, make sure you're assigned with the following access:
   * A policy with the Template Administrator role on All IAM Account Management services.
   * A policy with the Template Assignment Administrator role on All IAM Account Management services.

   By default, no users have the roles Template Administrator or Template Assignment Administrator, including the account owner.
   {: note}

- New and existing accounts in your enterprise must opt-in to enterprise-managed IAM. For more information, see [Opting in to enterprise-managed IAM](/docs/enterprise-management?topic=enterprise-management-enterprise-managed-opt-in).

## Creating an action control template
{: #create-act-ui}
{: ui}

You can create action control templates when you have many child accounts that require the same service restrictions. For example, as an enterprise IAM administrator, you want to restrict child account users from accounts from managing various settings for the Observability Routers.

To create an action control template, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates**, and select **Action controls** in the {{site.data.keyword.cloud_notm}} console.
1. Click **Create**.
1. Enter a name and description for the action control template that describes its purpose for enterprise users.
1. Enter the description for the action controls that describes its purpose for child account users.
1. Click **Create**, the template **Overview** page is displayed. To complete your template, you must configure the service on which you like to impose the restrictions.
1. Click **Configuration** tab, select a **Service**, and click **Next**.
1. Select the **Disallowed actions**. For example, if you select `logs-router.tenant.create`, your child account users cannot create a new tenant to the {{site.data.keyword.logs_routing_full_notm}}.
1. Click **Review** to verify your configuration, and click **Save** to update your template.
1. Click **Review** on the upper right of the template page. 
1. In the **Review and commit** page, select the confirmation to commit the template and click **commit**. Until you commit, the template is `Draft` state. After you commit, the template will be in `Committed` state.

You can assign templates to child accounts and account groups only after you commit. 
{: note}

## Assigning an action control template to child accounts
{: #assign-act-ui}
{: ui}

You can assign an action control templates to child accounts and account groups to restrict certain actions. To assign an action control template, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates**, and select **Action controls** in the {{site.data.keyword.cloud_notm}} console.
1. Select any action control template. 
1. Click **Assign accounts** on the upper right of the template page.
1. Select the accounts and account groups for which you like to assign the action control template.

If you select an account group, the template gets assigned to all current and future child accounts of that group.
{: note}

1. Click **Assign accounts** to assign the enterprise template to the specified accounts or account groups. 

## Updating an action control template
{: #update-act-ui}
{: ui}

To update an action control template, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates**, and select **Action controls** in the {{site.data.keyword.cloud_notm}} console.
1. Select any action control template.
1. Click **Assign accounts** to modify the assignments. You can change the specified accounts or account groups that are assigned to the template.

After you commit the templates, you will not be able to edit the template, but can create another version of the template. 
{: note}

## Creating a new version
{: #new-version-act-create-ui}
{: ui}

To create a new verson of the action control template, complete the following steps:

1. Go to **Manage > Access (IAM) > Templates**, and select **Action controls** in the {{site.data.keyword.cloud_notm}} console.
1. Select any action control template.
1. Click **Create new version** on the upper right of the template page.
1. Select the version based on which a new version of the template must be created.
1. Update the template and action control description, if necessary.
1. Select the action controls that you like to carry over to the new version.
1. Click **Create**. A new version of the template is created.
1. You can modify the configurations such as **Service** and **Disallowed actions** before you commit the template.
1. In the **Review and commit** page, select the confirmation to commit the template and click **commit**.
1. In the **Action controls** templates page, you can see a new version of the existing template.

## Updating a version
{: #update-assignment-act-ui}
{: ui}

To update a template assignment, follow these steps:

1. Go to **Manage > Access (IAM) > Templates**, and select **Action controls** in the {{site.data.keyword.cloud_notm}} console.
1. Select any action control template.
1. Click **Assignments** tab, for a particular assignment, click **Update** link.
1. Select the version and click **Update** to update the template version that is assigned to the child accounts.

## Removing an action control template assignment
{: #remove-assignment-settings-ui}
{: ui}

To remove a template assignment, follow these steps:

1. Go to **Manage > Access (IAM) > Templates**, and select **Action controls** in the {{site.data.keyword.cloud_notm}} console.
1. Select any action control template.
1. Click ![Actions](/icons/actions.jpg) icon, and click **Details** to view the assignment details.
1. On the **Assignment report** page, click **Unassign all**. 
1. You can also remove a template assignment from ![Actions](/icons/actions.jpg) icon, and select **Remove**.
1. Click **Remove** to confirm the removal of template assignment.

## Deleting an action control template
{: #delete-act-version-ui}
{: ui}

To delete a version of an action control template or delete an action control template, you must unassign all the assignments for the template. 
{: note}

To delete a template or template version, follow these steps:
1. Go to **Manage > Access (IAM) > Templates**, and select **Action controls** in the {{site.data.keyword.cloud_notm}} console.
1. For any particular template or template version, click ![Actions](/icons/actions.jpg) icon and select **Delete version** or **Delete template** respectively.
1. If you have not deleted the template assignments, select any action control template and remove all the assignments. 
1. Click ![Delete](/icons/delete.jpg) icon and click **Delete** to confirm the deletion of a template version.

## Creating an action control template by using the CLI
{: #create-act-cli}
{: cli}

Consider using action control templates when you have many child accounts that require the same service restrictions. For example, as an enterprise IAM administrator, you want to restrict child account users from accounts from managing various settings for the Observability Routers.

To create an action control template by using the CLI, complete the following steps:

1. Create a JSON file that configures the action control template definition. The following example JSON file specifies the `account_id` of the enterprise account, the `name` of the template. The `action_control.actions` argument specifies the action restrictions that are imposed on the child account. 

   ```json
   {
   "name": "Service controls template 4",
   "description": "Template description",
   "account_id": "f6c6c25cbe6b43d3b45198cc876a59ba",
   "action_control": {
      "actions": [
         "atracker.route.create",
         "atracker.route.update",
         "atracker.route.delete",
      ],
      "description": "Restrict access to atracker configurations",
      "service_name": "atracker"
   }
   }
   ```
   {: codeblock}

1. Create the action control template by using the `ibmcloud iam action-control-template-create` command as shown in the following sample request:

   ```bash
   ibmcloud iam action-control-template-create --file JSON_FILE [-f, --force] [-q, --quiet]
   ```
   {: codeblock}

   OPTIONS:
   - `--file` - JSON file of the action control template version definition
   - `-f`, `--force` - creates the template without confirmation
   - `-q`, `--quiet` - Suppresses the verbose output

## Deleting an action control template by using the CLI
{: #delete-act-cli}
{: cli}

To delete an action control template, use the following sample code:

```bash
ibmcloud iam action-control-template-version-delete TEMPLATE_ID|TEMPLATE_NAME TEMPLATE_VERSION [-f, --force]
```
{: codeblock}

- `-f` confirms the deletion of the template.

## Updating an action control template by using the CLI
{: #update-act-cli}
{: cli}

You can update an action control template at any time before you commit it. To update a specific version of an action control template, complete the following steps:

To update a specific version of an action control template, use the `action-control-template-version-update` command as shown in the following sample request:

   ```bash
   ibmcloud iam action-control-template-version-update TEMPLATE_NAME|TEMPLATE_ID TEMPLATE_VERSION --file /path/to/template/definition.
   ```
   {: codeblock}


## Assigning an action control template to child accounts by using the CLI
{: #assign-act-cli}
{: cli}

You can assign the versions of only one settings template at a time in your enterprise. You can assign different versions of the same settings template, but you can't use multiple settings templates in an enterprise. You might want to assign different versions to accounts with different requirements, like production and test accounts.

You can't assign an IAM template to the enterprise account, only child accounts.
{: note}

To create an assignment for an account settings template, complete the following steps:
1. List the settings templates in your enterprise account and note the template name and version number for the action control template that you want to assign to child accounts:

   ```bash
   ibmcloud iam action-control-templates
   ```
   {: codeblock}

1. Assign the template to an `Account` or `AccountGroup` by using the `action-control-assignment-create` command.

   ```bash
   ibmcloud iam action-control-assignment-create ActionControlTemplateUpdated 1 --target-type AccountGroup --target 955fc2274567474f8da802d5c376504b
   ```
   {: codeblock}

If an assignment fails, use the `action-control-assigment-update` method to retry.
{: tip}

## Retrieving versions of the action control template by using the CLI
{: #retrieve-version-act-cli}
{: cli}

To retrieve the versions of an action control template, you must be assigned one or more IAM access roles.

1. You can retrieve the latest version of an action control template by the providing an action control `template_id`.

   ```bash
   ibmcloud iam action-control-template TEMPLATE_NAME|TEMPLATE_ID
   ```
   {: codeblock}

1. You can retrieve all the versions of an action control template by providing an action control `template ID`.

   ```bash
   ibmcloud iam action-control-template-versions TEMPLATE_NAME|TEMPLATE_ID
   ```
   {: codeblock}

1. You can retrieve a specific version of an action control template by providing an action control `template ID` and `version`.

   ```bash
   ibmcloud iam action-control-template-version TEMPLATE_NAME|TEMPLATE_ID TEMPLATE_VERSION
   ```
   {: codeblock}

## Creating a new version by using the CLI
{: #new-version-act-create-cli}
{: cli}

Create a new version of an action control template when you need to make updates to a committed version. To create a new version, complete the following steps.

You can retrieve the latest version of an action control template by the providing an action control `template_id`.

```bash
ibmcloud iam action-control-template TEMPLATE_NAME|TEMPLATE_ID
```
{: codeblock}

Create a new version of an action control template when you need to make updates to a committed version. To create a new version, complete the following steps.

1. Update your JSON file with the new action control template configuration. For more information about the attributes that you can use in your JSON file, see the [IAM Policy Management API](/apidocs/iam-policy-management#replace-action-control-template).
1. Use the `iam-access-management.action-control-template.create` command to create a new version. The following sample request creates a new version of the template with template ID `actionControlTemplate-12345678-abcd-1a2b-a1b2-1234567890ab` for the `atracker` service.

   ```bash
   curl -X POST 'https://iam.cloud.ibm.com/v1/action_control_templates' \
   --header 'Content-Type: application/json' \
   --header 'Authorization: Bearer <TOKEN>' \
   --data '{
     "name": "Activity Tracker Event Routing restriction",
     "description": "Restrict access to manage target, route and setting configurations in child accounts",
     "account_id": "<ROOT_ENTERPRISE_ACCOUNT_ID>",
     "committed": true,
     "action_control": {
       "description": "Restrict access to atracker configurations",
       "service_name": "atracker",
       "actions": ["ACTION_ID_1", "ACTION_ID_2"]
       }
   }
   ```
   {: curl}
   {: codeblock}

## Updating a version by using the CLI
{: #update-assignment-act-cli}
{: cli}

Update an assignment to retry a failed assignment or migrate to a new version.

The new template version that you assign replaces the old version. Learn more about [Assigning a new version](/docs/enterprise-management?topic=enterprise-management-working-with-versions#new-version).
{: note}

1. List the assignments in the account by using the `action-control-assignments` method. Take note of the `ASSIGNMENT_ID` for the assignment that you want to update.
1. Update the action control assignment. If you're retrying an assignment, use the same version number. The following sample request migrates the assignment `actionControlAssignment-63d65ed159ff463b8ec09ea77d22a05b` to version 2.

   ```bash
   ibmcloud iam action-control-assignment-update actionControlAssignment-63d65ed159ff463b8ec09ea77d22a05b 2
   ```
   {: codeblock}

## Removing an action control template assignment by using the CLI
{: #remove-assignment-settings-cli}
{: cli}

You can remove a template assignment from an account or account group where the template is assigned. You might want to do so if the template isn't working as intended. When you remove a template assignment from an account, by default the previous version of the template is reinstated. If the assignment you remove is for the first or only version of a template, the enterprise-managed settings preferences in the child account are removed.

To remove an assignment, complete the following steps:

1. List the assignments in the account by using the `action-control-assignments` method. Take note of the `ASSIGNMENT_ID` for the assignment that you want to remove.
1. Remove the assignment by using the `action-control-assigment-delete` method. The following sample request removes the assignment `actionControlAssignment-63d65ed159ff463b8ec09ea77d22a05b`.

   ```bash
   ibmcloud iam action-control-assignment-delete actionControlAssignment-63d65ed159ff463b8ec09ea77d22a05b
   ```
   {: codeblock}

## Deleting a version by using the CLI
{: #delete-act-version-cli}
{: cli}

Before you can delete a settings template version, you must remove all assignments for that version of the template. Delete a specific version by completing the following steps:

1. List the settings templates in your enterprise account and note the template name and version number for the version that you want to delete:

   ```bash
   ibmcloud iam action-control-templates
   ```
   {: codeblock}

1. Delete the version:

   ```bash
   ibmcloud iam action-control-template-delete ActionControlTemplateUpdated 2
   ```
   {: #codeblock}

1. To delete all versions, repeat these steps. Make sure that you remove the assignments for each version first.


## Creating an action control template by using the API
{: #create-act-api}
{: api}

Consider using action control templates when you have many child accounts that require the same service restrictions. For example, as an enterprise IAM administrator, you want to restrict child account users from deleting the auditing events from {{site.data.keyword.atracker_short}}.

To create an action control template by using the API, complete the following steps:

Create a JSON file that configures the template definition. For more information about the attributes that you can use in your JSON file, see the [IAM Policy Management API](/apidocs/iam-policy-management#list-action-control-templates). The following example JSON file specifies the `account_id` of the enterprise account, the `name` of the template. 

```bash
   curl -X POST 'https://iam.test.cloud.ibm.com/v1/action_control_templates' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json' -d '{
   "name": "Billing discounts",
   "description": "Restrict access to manage target setting configurations in child accounts",
   "account_id": "ROOT_ENTERPRISE_ACCOUNT_ID",
   "action_control": {
    "description": "Restrict access to atracker configurations",
    "service_name": "atracker",
    "actions": [ "atracker.setting.update",
            "atracker.target.create",
            "atracker.target.update",
            "atracker.target.delete",
         }
   }'
```
{: curl}
{: codeblock}

```java
   ServiceCall<ActionControlTemplate> createActionControlTemplate(CreateActionControlTemplateOptions createActionControlTemplateOptions)
```
{: java}
{: codeblock}
   
```javascript
   createActionControlTemplate(params)
```
{: javascript}
{: codeblock}

```Python
   create_action_control_template(
   self,
   name: str,
   account_id: str,
   *,
   description: Optional[str] = None,
   committed: Optional[bool] = None,
   action_control: Optional['TemplateActionControl'] = None,
   accept_language: Optional[str] = None,
   **kwargs,
   )
```
{: python}
{: codeblock}

```go
(iamPolicyManagement *IamPolicyManagementV1) CreateActionControlTemplate(createActionControlTemplateOptions *CreateActionControlTemplateOptions) (result *ActionControlTemplate, response *core.DetailedResponse, err error)

(iamPolicyManagement *IamPolicyManagementV1) CreateActionControlTemplateWithContext(ctx context.Context, createActionControlTemplateOptions *CreateActionControlTemplateOptions) (result *ActionControlTemplate, response *core.DetailedResponse, err error)
   ```
{: go}
{: codeblock}

## Deleting an action control template by using the API
{: #delete-act-API}
{: api}

Before you delete an action control template, you must remove the action control assignments. An action control template can't be deleted if any version of the template is assigned to one or more child accounts. To delete an action control template, complete the following steps:

To delete an action control template, you must be assigned one or more IAM access roles that include the following action.
`iam-access-management.action-control-template.delete`

An action control template can be deleted by providing the action control template ID. The following example JSON file specifies the `template_id` of the action control template.

```bash
   curl -X DELETE 'https://iam.test.cloud.ibm.com/v1/action_control_templates/$TEMPLATE_ID' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json'
```
{: curl}
{: codeblock}

```java
   ServiceCall<Void> deleteActionControlTemplate(DeleteActionControlTemplateOptions deleteActionControlTemplateOptions)
```
{: java}
{: codeblock}
   
```javascript
   deleteActionControlTemplate(params)
```
{: javascript}
{: codeblock}

```Python
   delete_action_control_template(
   self,
   action_control_template_id: str,
   **kwargs,
   ) -> DetailedResponse
```
{: python}
{: codeblock}

```go
(iamPolicyManagement *IamPolicyManagementV1) DeleteActionControlTemplate(deleteActionControlTemplateOptions *DeleteActionControlTemplateOptions) (response *core.DetailedResponse, err error)

(iamPolicyManagement *IamPolicyManagementV1) DeleteActionControlTemplateWithContext(ctx context.Context, deleteActionControlTemplateOptions *DeleteActionControlTemplateOptions) (response *core.DetailedResponse, err error)
   ```
{: go}
{: codeblock}

When you delete an action control template, all versions of this template are deleted.
{: note}

## Retrieving versions of the action control template by using the API
{: #retrieve-version-act-API}
{: api}

To retrieve the versions of an action control template, you must be assigned one or more IAM access roles that include the following action.
`iam-access-management.action-control-template.read`.

- You can retrieve the latest version of an action control template by the providing an action control `template_id`.

```bash
curl -X GET 'https://iam.test.cloud.ibm.com/v1/action_control_templates/$TEMPLATE_ID&state=active' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json'
```
{: curl}
{: codeblock}

```java
ServiceCall<ActionControlTemplate> getActionControlTemplate(GetActionControlTemplateOptions getActionControlTemplateOptions)
```
{: java}
{: codeblock}

```javascript
getActionControlTemplate(params)
```
{: javascript}
{: codeblock}

```python
get_action_control_template(
        self,
        action_control_template_id: str,
        *,
        state: Optional[str] = None,
        **kwargs,
    ) -> DetailedResponse
```
{: python}
{: codeblock}

```go
(iamPolicyManagement *IamPolicyManagementV1) GetActionControlTemplate(getActionControlTemplateOptions *GetActionControlTemplateOptions) (result *ActionControlTemplate, response *core.DetailedResponse, err error)

(iamPolicyManagement *IamPolicyManagementV1) GetActionControlTemplateWithContext(ctx context.Context, getActionControlTemplateOptions *GetActionControlTemplateOptions) (result *ActionControlTemplate, response *core.DetailedResponse, err error)
```
{: go}
{: codeblock}

- You can retrieve all the versions of an action control template by providing an action control `template ID`.

```bash
curl -X GET 'https://iam.test.cloud.ibm.com/v1/action_control_templates/$TEMPLATE_ID/versions&state=active' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json'
```
{: curl}
{: codeblock}

```java
ServiceCall<ActionControlTemplateVersionsCollection> listActionControlTemplateVersions(ListActionControlTemplateVersionsOptions listActionControlTemplateVersionsOptions)
```
{: java}
{: codeblock}

```javascript
listActionControlTemplateVersions(params)
```
{: javascript}
{: codeblock}

```python
list_action_control_template_versions(
        self,
        action_control_template_id: str,
        *,
        state: Optional[str] = None,
        limit: Optional[int] = None,
        start: Optional[str] = None,
        **kwargs,
    ) -> DetailedResponse
```
{: python}
{: codeblock}

```Go
(iamPolicyManagement *IamPolicyManagementV1) ListActionControlTemplateVersions(listActionControlTemplateVersionsOptions *ListActionControlTemplateVersionsOptions) (result *ActionControlTemplateVersionsCollection, response *core.DetailedResponse, err error)

(iamPolicyManagement *IamPolicyManagementV1) ListActionControlTemplateVersionsWithContext(ctx context.Context, listActionControlTemplateVersionsOptions *ListActionControlTemplateVersionsOptions) (result *ActionControlTemplateVersionsCollection, response *core.DetailedResponse, err error)
```
{: go}
{: codeblock}

- You can retrieve a specific version of an action control template by providing an action control `template ID` and `version`.

```bash
curl -X GET 'https://iam.test.cloud.ibm.com/v1/action_control_templates/$TEMPLATE_ID/versions/$TEMPLATE_VERSION' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json'
```
{: curl}
{: codeblock}

```java
ServiceCall<ActionControlTemplate> getActionControlTemplateVersion(GetActionControlTemplateVersionOptions getActionControlTemplateVersionOptions)
```
{: java}
{: codeblock}

```javascript
getActionControlTemplateVersion(params)
```
{: javascript}
{: codeblock}

```python
get_action_control_template_version(
        self,
        action_control_template_id: str,
        version: str,
        **kwargs,
    ) -> DetailedResponse
```
{: python}
{: codeblock}

```Go
(iamPolicyManagement *IamPolicyManagementV1) GetActionControlTemplateVersion(getActionControlTemplateVersionOptions *GetActionControlTemplateVersionOptions) (result *ActionControlTemplate, response *core.DetailedResponse, err error)

(iamPolicyManagement *IamPolicyManagementV1) GetActionControlTemplateVersionWithContext(ctx context.Context, getActionControlTemplateVersionOptions *GetActionControlTemplateVersionOptions) (result *ActionControlTemplate, response *core.DetailedResponse, err error)
```
{: go}
{: codeblock}

## Creating a new version by using the API
{: #new-version-create-API}
{: api}

Create a new version of an action control template when you need to make updates to a committed version. To create a new version, complete the following steps.

1. Update your JSON file with the new action control template configuration. For more information about the attributes that you can use in your JSON file, see the [IAM Policy Management API](/apidocs/iam-policy-management#replace-action-control-template).
1. Use the `iam-access-management.action-control-template.create` method to create a new version. The following sample request creates a new version of the template with template ID `actionControlTemplate-12345678-abcd-1a2b-a1b2-1234567890ab` for the `atracker` service.

```bash
   curl -X POST 'https://iam.test.cloud.ibm.com/v1/action_control_template/$TEMPLATE_ID/versions' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json' -d '{
   "name": "Activity Tracker Event Routing restriction",
   "description": "Restrict access to atracker configurations",
   "action_control": {
   "description": "Restrict access to atracker configurations",
   "service_name": "atracker",
   "actions": ["ACTION_ID_1", "ACTION_ID_2"]
   }
   }'
```
{: curl}
{: codeblock}

```java
ServiceCall<ActionControlTemplate> createActionControlTemplateVersion(CreateActionControlTemplateVersionOptions createActionControlTemplateVersionOptions)
```
{: java}
{: codeblock}

```javascript
createActionControlTemplateVersion(params)
```
{: javascript}
{: codeblock}

```python
   create_action_control_template_version(
   self,
   action_control_template_id: str,
   action_control: 'TemplateActionControl',
   *,
   name: Optional[str] = None,
   description: Optional[str] = None,
   committed: Optional[bool] = None,
   **kwargs,
    ) -> DetailedResponse
```
{: python}
{: codeblock}

```go
(iamPolicyManagement *IamPolicyManagementV1) CreateActionControlTemplateVersion(createActionControlTemplateVersionOptions *CreateActionControlTemplateVersionOptions) (result *ActionControlTemplate, response *core.DetailedResponse, err error)

(iamPolicyManagement *IamPolicyManagementV1) CreateActionControlTemplateVersionWithContext(ctx context.Context, createActionControlTemplateVersionOptions *CreateActionControlTemplateVersionOptions) (result *ActionControlTemplate, response *core.DetailedResponse, err error)
```
{: go}
{: codeblock}

## Updating a version by using the API
{: #update-act-API}
{: api}

You can update a specific version of an action control template, only if the version is not committed. 

The new template version that you assign replaces the old version. Learn more about [Assigning an action control template](/apidocs/iam-policy-management#create-action-control-template-assignment).
{: note}

Use the `iam-access-management.action-control-template.update` method to update a new version. The following sample request creates a new version of the template with the same template ID `actionControlTemplate-12345678-abcd-1a2b-a1b2-1234567890ab`, but version: `1` for the `atracker` service.

   ```bash
   curl -X PUT 'https://iam.test.cloud.ibm.com/v1/action_control_templates/$TEMPLATE_ID/versions/$TEMPLATE_VERSION' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json' -H 'If-Match: $ETAG' -d '{
    "name": "Billing discounts",
    "description": "Restrict access to atracker configurations",
    "action_control": {
     "description": "Restrict access to atracker configurations",
     "service_name": "atracker",
     "actions": ["ACTION_ID_1", "ACTION_ID_2"]
    }
   }'
   ```
{: curl}
{: codeblock}

```java
ServiceCall<ActionControlTemplate> replaceActionControlTemplate(ReplaceActionControlTemplateOptions replaceActionControlTemplateOptions)
```
{: java}
{: codeblock}

```javascript
replaceActionControlTemplate(params)
```
{: javascript}
{: codeblock}

```python
replace_action_control_template(
        self,
        action_control_template_id: str,
        version: str,
        if_match: str,
        action_control: 'TemplateActionControl',
        *,
        name: Optional[str] = None,
        description: Optional[str] = None,
        committed: Optional[bool] = None,
        **kwargs,
    ) -> DetailedResponse
```
{: python}
{: codeblock}

```go
   (iamPolicyManagement *IamPolicyManagementV1) ReplaceActionControlTemplate(replaceActionControlTemplateOptions *ReplaceActionControlTemplateOptions) (result *ActionControlTemplate, response *core.DetailedResponse, err error)

   (iamPolicyManagement *IamPolicyManagementV1) ReplaceActionControlTemplateWithContext(ctx context.Context, replaceActionControlTemplateOptions *ReplaceActionControlTemplateOptions) (result *ActionControlTemplate, response *core.DetailedResponse, err error)
```
{: go}
{: codeblock}

## Deleting a version by using the API
{: #delete-act-version-API}
{: api}

Before you can delete an action control template version, you must remove all action control assignments for that version of the template. You can't delete an action control template version that is assigned to one or more child accounts. 

1. To delete a specific version of an action control template, provide an action control `template ID` and `version number`. 
1. Use the `iam-access-management.action-control-template.delete` method to delete a version of the action control template. The following sample request deletes the specified version of the action control template.

```bash
   DELETE /v1/action_control_templates/{action_control_template_id}/versions/{version}
   ```
{: curl}
{: codeblock}

```java
ServiceCall<Void> deleteActionControlTemplateVersion(DeleteActionControlTemplateVersionOptions deleteActionControlTemplateVersionOptions)
```
{: java}
{: codeblock}

```javascript
deleteActionControlTemplateVersion(params)
```
{: javascript}
{: codeblock}

```python
delete_action_control_template_version(
        self,
        action_control_template_id: str,
        version: str,
        **kwargs,
    ) -> DetailedResponse
```
{: python}
{: codeblock}

```go
   (iamPolicyManagement *IamPolicyManagementV1) DeleteActionControlTemplateVersion(deleteActionControlTemplateVersionOptions *DeleteActionControlTemplateVersionOptions) (response *core.DetailedResponse, err error)

   (iamPolicyManagement *IamPolicyManagementV1) DeleteActionControlTemplateVersionWithContext(ctx context.Context, deleteActionControlTemplateVersionOptions *DeleteActionControlTemplateVersionOptions) (response *core.DetailedResponse, err error)
```
{: go}
{: codeblock}

1. To delete all versions, repeat these steps. Make sure that you remove the assignments for each version first.

## Committing an action control template version by using the API
{: #commit-act-version-API}
{: api}

After committing an action control template version, you cannot make any further changes to the action control template. If you must make updates after committing a version, create a new version of the template.

Use the `iam-access-management.action-control-template.update` method to commit a version of the action control template. The following sample request commits a version of the action control template.

   ```bash
   curl -X POST 'https://iam.test.cloud.ibm.com/v1/action_control_templates/$TEMPLATE_ID/versions/$TEMLPATE_VERSION/commit' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json' -d '{}'
   ```
   {: curl}
   {: codeblock}

   ```java
   ServiceCall<Void> commitActionControlTemplate(CommitActionControlTemplateOptions commitActionControlTemplateOptions)
   ```
   {: java}
   {: codeblock}

   ```javascript
   commitActionControlTemplate(params)
   ```
   {: javascript}
   {: codeblock}

   ```Python
   commit_action_control_template(
   self,
   action_control_template_id: str,
   version: str,
   **kwargs,
   ) -> DetailedResponse
   ```
   {: python}
   {: codeblock}

   ```go
   (iamPolicyManagement *IamPolicyManagementV1) CommitActionControlTemplate(commitActionControlTemplateOptions *CommitActionControlTemplateOptions) (response *core.DetailedResponse, err error)

   (iamPolicyManagement *IamPolicyManagementV1) CommitActionControlTemplateWithContext(ctx context.Context, commitActionControlTemplateOptions *CommitActionControlTemplateOptions) (response *core.DetailedResponse, err error)
   ```
   {: go}
   {: codeblock}

## Assigning an action control template to child accounts by using the API
{: #assign-act-API}
{: api}

You can assign the versions of only one action control template at a time in your enterprise. You can assign different versions of the same action control template, but you can't use multiple action control templates in an enterprise. You might want to assign different versions to accounts with different requirements, like production and test accounts.

You can't assign an IAM action control template to the enterprise account. You can assign them only to the child accounts.
{: note}

- List the action control template assignments in your enterprise account and note the template name and version number for the action control template that you want to assign to child accounts:

  ```bash
   curl -X GET 'https://iam.test.cloud.ibm.com/v1/action_control_assignments?account_id=$ACCOUNT_ID' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json'
   ```
   {: curl}
   {: codeblock}

   ```java
   ServiceCall<ActionControlAssignmentCollection> listActionControlAssignments(ListActionControlAssignmentsOptions listActionControlAssignmentsOptions)
   ```
   {: java}
   {: codeblock}

   ```javascript
   listActionControlAssignments(params)
   ```
   {: javascript}
   {: codeblock}

   ```python
   list_action_control_assignments(
        self,
        account_id: str,
        *,
        accept_language: Optional[str] = None,
        template_id: Optional[str] = None,
        template_version: Optional[str] = None,
        limit: Optional[int] = None,
        start: Optional[str] = None,
        **kwargs,
    ) -> DetailedResponse
    ```
   {: python}
   {: codeblock}

   ```go
    (iamPolicyManagement *IamPolicyManagementV1) ListActionControlAssignments(listActionControlAssignmentsOptions *ListActionControlAssignmentsOptions) (result *ActionControlAssignmentCollection, response *core.DetailedResponse, err error)

    (iamPolicyManagement *IamPolicyManagementV1) ListActionControlAssignmentsWithContext(ctx context.Context, listActionControlAssignmentsOptions *ListActionControlAssignmentsOptions) (result *ActionControlAssignmentCollection, response *core.DetailedResponse, err error)
    ```
   {: go}
   {: codeblock}

- You can get a specific action control template assignment by providing an action control `assignment ID`.

   ```bash
      curl -X GET 'https://iam.test.cloud.ibm.com/v1/action_control_assignments/$ASSIGNMENT_ID' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json'
   ```
   {: curl}
   {: codeblock}

   ```java
   ServiceCall<ActionControlAssignment> getActionControlAssignment(GetActionControlAssignmentOptions getActionControlAssignmentOptions)
   ```
   {: java}
   {: codeblock}

   ```javascript
   getActionControlAssignment(params)
   ```
   {: javascript}
   {: codeblock}

   ```python
   get_action_control_assignment(
        self,
        assignment_id: str,
        **kwargs,
    ) -> DetailedResponse
    ```
   {: python}
   {: codeblock}

   ```go
    (iamPolicyManagement *IamPolicyManagementV1) GetActionControlAssignment(getActionControlAssignmentOptions *GetActionControlAssignmentOptions) (result *ActionControlAssignment, response *core.DetailedResponse, err error)

    (iamPolicyManagement *IamPolicyManagementV1) GetActionControlAssignmentWithContext(ctx context.Context, getActionControlAssignmentOptions *GetActionControlAssignmentOptions) (result *ActionControlAssignment, response *core.DetailedResponse, err error)
    ```
   {: go}
   {: codeblock}

- Use the `iam-access-management.action-control-assignment.create` command to assign the template to an `account` or `account group`. The following sample request assigns an action control template to a target account.

   ```bash
   curl -X POST 'https://iam.test.cloud.ibm.com/v1/action_control_assignments' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json' -d '{
      "templates": [{
      "id": "template_id",
      "version": "template_version"
    }],
    "target": {
    "id": "target account",
    "type": "target type"
    }
   }'
   ```
   {: curl}
   {: codeblock}

   ```java
   ServiceCall<ActionControlAssignmentCollection> createActionControlTemplateAssignment(CreateActionControlTemplateAssignmentOptions createActionControlTemplateAssignmentOptions)
   ```
   {: java}
   {: codeblock}

   ```javascript
   createActionControlTemplateAssignment(params)
   ```
   {: javascript}
   {: codeblock}

   ```Python
   create_action_control_template_assignment(
        self,
        target: 'AssignmentTargetDetails',
        templates: List['ActionControlAssignmentTemplate'],
        *,
        accept_language: Optional[str] = None,
        **kwargs,
    ) -> DetailedResponse
   ```
   {: python}
   {: codeblock}

   ```GO
   (iamPolicyManagement *IamPolicyManagementV1) CreateActionControlTemplateAssignment(createActionControlTemplateAssignmentOptions *CreateActionControlTemplateAssignmentOptions) (result *ActionControlAssignmentCollection, response *core.DetailedResponse, err error)

    (iamPolicyManagement *IamPolicyManagementV1) CreateActionControlTemplateAssignmentWithContext(ctx context.Context, createActionControlTemplateAssignmentOptions *CreateActionControlTemplateAssignmentOptions) (result *ActionControlAssignmentCollection, response *core.DetailedResponse, err error)
   ```
   {: go}
   {: codeblock}

If an assignment fails, use the `iam-access-management.action-control-assignment.update` method to retry.
{: tip}

## Removing an action control assignments by using the API
{: #remove-act-API}
{: api}

You can remove a template assignment by providing an action control `assignment ID`. You can't delete an action control assignment if the status is `in_progress`.

```bash
DELETE /v1/action_control_assignments/{assignment_id}
```
{: curl}
{: codeblock}

```java
ServiceCall<Void> deleteActionControlAssignment(DeleteActionControlAssignmentOptions deleteActionControlAssignmentOptions)
```
{: java}
{: codeblock}

```javascript
deleteActionControlAssignment(params)
```
{: javascript}
{: codeblock}

```python
delete_action_control_assignment(
self,
assignment_id: str,
**kwargs,
) -> DetailedResponse
```
{: python}
{: codeblock}

```go
(iamPolicyManagement *IamPolicyManagementV1) DeleteActionControlAssignment(deleteActionControlAssignmentOptions *DeleteActionControlAssignmentOptions) (response *core.DetailedResponse, err error)

(iamPolicyManagement *IamPolicyManagementV1) DeleteActionControlAssignmentWithContext(ctx context.Context, deleteActionControlAssignmentOptions *DeleteActionControlAssignmentOptions) (response *core.DetailedResponse, err error)
```
{: go}
{: codeblock}

## Creating an action control template by using Terraform
{: #create-act-terraform}
{: terraform}

Before you create an action control template by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

Use the following steps to create an action control template by using the terraform. 
1. In your terraform configuration file, define the resource by using `ibm_iam_action_control_template`. 
1. Create an argument `action_control` with the `actions` property and `am-test-service.test.create` command. The following example creates an action control template for the `am-test-service` service, where `name` is the name of the new action control template. 

```terraform
 resource "ibm_iam_action_control_template" "action_control_template_instance" {
   name = "TestTemplates"
   description = "Base template Testing"
   action_control {
   actions = ["am-test-service.test.create" ]
   service_name="am-test-service"
   }
   committed = "true"
}
```
{: codeblock}

To commit a version of the action control template, set `committed` to `true`.

After committing an action control template, you cannot make any further changes to the action control template. If you must make updates after committing a version, create a new version of the template.
{: note}

## Deleting an action control template by using Terraform
{: #delete-act-terraform}
{: terraform}

The following example deletes an action control template `TerraformActionControlTest` for the `service`.

```terraform
      resource "ibm_iam_action_control_template" "action_template" {
   	name = "TerraformActionControlTest"
    	action_control {
    		actions = ["am-test-service.test.delete" ]
    		service_name="am-test-service"
     		}
	committed=true
}
```
{: codeblock}

## Creating a new version by using Terraform
{: #new-version-create-terraform}
{: terraform}

Create a new version of an action control template when you need to make updates to a committed version. To create a new version, complete the following steps.

1. In your terraform configuration file, define the resource by using `ibm_iam_action_control_template_version`. 
1. Create an argument `action_control` with the `actions` property and `am-test-service.test.create` command. The following example creates a new version (`action_control_template_v2`) of an existing action control template `action_control_template_v1`. `action_control_template_id` defines the template ID of the new version of the action control template.

```terraform
resource "ibm_iam_action_control_template_version" "action_control_template_v2" {
   action_control_template_id = ibm_iam_action_control_template.action_control_template_v1.action_control_template_id
   description = "Template description"
   action_control {
   actions = ["am-test-service.test.create" ]
   service_name="am-test-service"
   }
   committed = "true"
}
```
{: codeblock}


## Updating a version by using Terraform
{: #update-act-terraform}
{: terraform}

Update an assignment to retry a failed assignment or migrate to a new version.

The new template version that you assign replaces the old version. Learn more about [Assigning a new version](/docs/enterprise-management?topic=enterprise-management-working-with-versions#new-version).
{: note}

If you're retrying an assignment, use the same version number. The following sample request migrates the assignment `ibm_iam_action_control_template.template` to version 2.

   ```terraform
   resource "ibm_iam_action_control_assignment" "assignment" {
		  target  ={
		  type = "Account"
		  id = "0ddc8e9eb0894383b48791ff4ba0b80e"
	     }
		  templates{
		   id = ibm_iam_action_control_template.template.action_control_template_id 
		   version = ibm_iam_action_control_template.template.version  
	   }
      template_version="2"
   }
   ```
   {: codeblock}


## Deleting a version by using Terraform
{: #delete-act-version-terraform}
{: terraform}

Before you can delete an action control template version, you must remove all assignments for that version of the template. Delete a specific version by completing the following steps:

Make a note of the template name and version number of the version that you want to delete and delete the version. The following example deletes a `template_version`.

   ```terraform
   resource "ibm_iam_action_control_template_version" "template_version" {
   action_control_template_id = ibm_iam_action_control_template.template.action_control_template_id
   action_control {
   actions = ["am-test-service.test.delete" ]
   service_name="am-test-service"
   }   
   committed = true
   }
   ```
   {: codeblock}

To delete all versions, repeat these steps. Make sure that you remove the assignments for each version first.
{: note}

## Assigning an action control template by using Terraform
{: #assign-act-terraform}
{: terraform}

You can assign the versions of only one action control template at a time in your enterprise. You can assign different versions of the same action control template, but you can't use multiple action control templates in an enterprise. You might want to assign different versions to accounts with different requirements, like production and test accounts.

To create an assignment for an action control template, assign an action control template to the particular enterprise account. The following example assigns an action control template to the `Enterprise`.

   ```terraform
   resource "ibm_iam_action_control_assignment" "action_control_assignment" {
	target  ={
   		type = "Enterprise"
    		id = "<target-enterpriseId>"
	}
	
	templates{
    		id = ibm_iam_action_control_template.action_template.template_id 
   		version = ibm_iam_action_control_template.action_template.version
	}
	template_version=ibm_iam_action_control_template_version.template_version.version
   }
   ```
   {: codeblock}
