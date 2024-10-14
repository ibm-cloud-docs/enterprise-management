---

copyright:
  years: 2020, 2023
lastupdated: "2024-10-14"

keywords: enterprise, add account, import account, create account

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}


# Adding accounts to an enterprise
{: #enterprise-add}

You can build out your enterprise by adding more {{site.data.keyword.Bluemix}} accounts to it. To add accounts, you can import existing accounts that aren't in another enterprise, or you can create new accounts within your enterprise.
{: shortdesc}

After your enterprise has multiple accounts, you can organize related accounts by using account groups. For more information, see in [Organizing accounts in an enterprise](/docs/enterprise-management?topic=enterprise-management-enterprise-organize).

You can have up to 1000 accounts in an enterprise. For more information, see [Enterprise limits](/docs/enterprise-management?topic=enterprise-management-known-issues#enterprise-limits).
{: note}

## Importing existing accounts
{: #add-accounts}

You can import existing accounts into an enterprise. After you import an account, it can't be removed, and each account can be a part of only one enterprise. If you import a Lite or trial account, it's automatically upgraded to a [Pay-As-You-Go account](/docs/account?topic=account-accounts).

Importing an account to the enterprise has the following impacts:
* Billing for the account transitions to being managed by the enterprise. After the transition, users in the account can't access billing and payment information, such as invoices, payments, or subscriptions, for future billing periods. To view or manage billing, users need to be invited to the enterprise account and be given access to the Billing service in that account. See [Centrally manage billing and usage with enterprises](/docs/enterprise-management?topic=enterprise-management-enterprise) for more information.
* Users and access permissions within the account are not changed. Access within the account is separate from the enterprise, and users don't automatically get access within the enterprise when the account is imported.
* Resources within the account are not changed. Users with the correct access permissions can continue to view usage information for resources in the account.

To import existing accounts into an enterprise, the following access is required:

   * Within the account to be imported, you must be the account owner or have the Administrator role on the Billing service within the account.
   * Within the enterprise account, you need the Editor or Administrator role on the Enterprise service and the Administrator role on the Billing service.

### Importing an account in the console
{: #add-accoun-ui}
{: ui}

To import an existing account, complete the following steps:


1. Log in to your enterprise account, and go to **Manage > Enterprise** in the {{site.data.keyword.Bluemix_notm}} console.
1. Click **Accounts** to view the accounts and account groups in the enterprise. In the Accounts section, select **Add > Import account**.
1. Select the account that you want to import.

   If no accounts are displayed, you likely don't have the correct access in any existing accounts.
   {: tip}

1. If you want to add the account to an account group, select the account group to be its parent. The parent that you select determines where in the enterprise hierarchy the account exists.
1. Review the information about impacts to your account, and select **I understand the impact to my account**. Then, click **Import**.

   After the account is imported to the enterprise, it can't be removed. Be sure you want to permanently move the account to the enterprise.
   {: important}

### Importing accounts by using the CLI
{: #add-account-cli}
{: cli}

1. Find the ID of the account that you want to import to the enterprise.

   ```bash
   ibmcloud account list
   ```
   {: codeblock}

1. If you want to add the account to an account group, find the names and IDs of existing account groups in the enterprise.

   ```bash
   ibmcloud enterprise account-groups --recursive
   ```
   {: codeblock}

1. Import the account into the enterprise, specifying the account ID for the `--account ID` parameter. If you don't specify a parent account group, the account is added directly under the enterprise.

   ```bash
   ibmcloud enterprise account-import --account-id ID
   [--parent-account-group ACCOUNT_GROUP_NAME | --parent-account-group-id ACCOUNT_GROUP_ID]
   ```
   {: codeblock}

### Importing accounts by using the API
{: #add-account-api}
{: api}

To import an existing account to the enterprise, call the [Enterprise Management API](/apidocs/enterprise-apis/enterprise#import-account-to-enterprise){: external} as shown in the following sample request. Replace the {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) token and ID variables with the values from your enterprise.

```bash
curl -X PUT "https://enterprise.cloud.ibm.com/v1/enterprises/$ENTERPRISE_ID/import/accounts/$ACCOUNT_ID" -H "Authorization: Bearer <IAM_Token>" -H 'Content-Type: application/json' -d '{
   "parent": "crn:v1:bluemix:public:enterprise::a/$ENTERPRISE_ACCOUNT_ID::enterprise:$ENTERPRISE_ID",
   "billing_unit_id": "$BILLING_UNIT_ID"
}'
```
{: codeblock}
{: curl}


```java
ImportAccountToEnterpriseOptions importAccountToEnterpriseOptions = new ImportAccountToEnterpriseOptions.Builder()
    .enterpriseId(enterpriseId)
    .accountId(importAccountId)
    .build();

Response<Void> response = service.importAccountToEnterprise(importAccountToEnterpriseOptions).execute();
```
{: codeblock}
{: java}


```javascript
const params = {
   enterpriseId: enterpriseId,
   accountId: importAccountId,
};

enterpriseManagementService.importAccountToEnterprise(params)
   .then(res => {
    done();
   })
   .catch(err => {
    console.warn(err)
   });
```
{: codeblock}
{: javascript}


```python
response = enterprise_management_service.import_account_to_enterprise(
   enterprise_id=enterprise_id,
   account_id=import_account_id,
)

print(json.dumps(response, indent=2))
```
{: codeblock}
{: python}


```go
importAccountToEnterpriseOptions := enterpriseManagementService.NewImportAccountToEnterpriseOptions(
   enterpriseID,
   importAccountID,
)

response, err := enterpriseManagementService.ImportAccountToEnterprise(importAccountToEnterpriseOptions)
if err != nil {
   panic(err)
}
```
{: codeblock}
{: go}


## Before you begin
{: #add-account-terraform-prereq}
{: terraform}

Before you can add accounts to an enterprise by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

### Importing accounts by using Terraform
{: #add-account-terraform}
{: terraform}

Use the following steps to import an existing account in an enterprise resource by using Terraform.

1. Create an argument in your `main.tf` file. The following example imports an account by using the `ibm_enterprise_account` resource, where `enterprise_id` is where the account is imported. You must have an existing IAM ID of an enterprise primary contact in order to complete the task.

   ```terraform
   resource "ibm_enterprise_account" "enterprise_import_account"{
    parent = "parent"
    enterprise_id = "enterprise_id"
    account_id = "account_id"
    }
    ```
   {: codeblock}

   You can specify the ID of an account that needs to be imported on the `account_id` option. For more information, see the argument reference details on the [Terraform Enterprise Management](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/enterprise_account){: external} page.

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

## Creating new accounts
{: #create-accounts}

You can create new accounts within your enterprise. The accounts are created as Pay-As-You-Go accounts, and usage is billed to the enterprise. To create an account, you need an access policy with the Editor or Administrator role on the Enterprise service.

### Creating accounts in the console
{: #create-account-ui}
{: ui}

1. From the Enterprise dashboard, click **Accounts** to view accounts and account groups in the enterprise.
1. In the Accounts section, select **Add > Create account**.
1. Enter a name for the account that's unique within the enterprise. Because it's one of many accounts, a unique, descriptive name helps you understand the purpose of the account at a glance.
1. If you want to assign a different user as the account owner, enter their IBMid in the **Owner** field. The account owner has full access to manage the account.
1. If you want to add the account to an account group, select the account group to be its parent. The parent that you choose determines where in the enterprise hierarchy the account exists.
1. Turn on **Enterprise-managed IAM** to centrally manage access and security settings in the new account. For more information, see [Opting in to enterprise-managed IAM](/docs/enterprise-management?topic=enterprise-management-enterprise-managed-opt-in).
1. Click **Create**.

After you create the account, the account owner can log in to the account to invite other users and manage their access.

### Creating accounts by using the CLI
{: #create-accounts-cli}
{: cli}

1. If you want to add the account to an account group, find the names and IDs of existing account groups.

   ```bash
   ibmcloud enterprise account-groups --recursive
   ```
   {: codeblock}

1. Create the account by running the following command. If you don't specify a parent account group, the account is added directly under the enterprise. To make a different user the account owner, specify their IBMid on the `--owner` option.

   ```bash
   ibmcloud enterprise account-create NAME
   [--parent-account-group ACCOUNT_GROUP_NAME] [--owner USER_ID]
   ```
   {: codeblock}

### Creating accounts by using the API
{: #create-account-api}
{: api}

To create a new account in the enterprise, call the Enterprise Management API as shown in the following sample request, replacing the IAM token and ID variables with the values from your enterprise. For detailed information about the API, see [Enterprise Management API](/apidocs/enterprise-apis/enterprise#create-account){: external}.

```bash
curl -X POST "https://enterprise.cloud.ibm.com/v1/accounts
-H "Authorization: Bearer <IAM_Token>"
-H 'Content-Type: application/json'
-d '{
  "parent":
  "crn:v1:bluemix:public:enterprise::a/$ENTERPRISE_ACCOUNT_ID::account-group:$ACCOUNT_GROUP_ID",
  "name": "Example Account",
  "owner_iam_id": "$OWNER_IAM_ID"
}'
```
{: codeblock}
{: curl}

```java
CreateAccountOptions createAccountOptions = new CreateAccountOptions.Builder()
    .parent(parentCRN)
    .name("Example Account")
    .ownerIamId(enterpriseAccountIamId)
    .build();

Response<CreateAccountResponse> response = service.createAccount(createAccountOptions).execute();
CreateAccountResponse createAccountResponse = response.getResult();

System.out.println(createAccountResponse);();
```
{: codeblock}
{: java}

```javascript
const params = {
  parent: parentCrn,
  name: 'Example Account',
  ownerIamId: enterpriseAccountIamId,
};

enterpriseManagementService.createAccount(params)
  .then(res => {
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: codeblock}
{: javascript}

```python
create_account_response = enterprise_management_service.create_account(
  parent=parent_crn,
  name='Example Account',
  owner_iam_id=enterprise_account_iam_id,
).get_result()

print(json.dumps(create_account_response, indent=2))
```
{: codeblock}
{: python}

```go
createAccountOptions := enterpriseManagementService.NewCreateAccountOptions(
  parentCRN,
  "Example Account",
  enterpriseAccountIamID,
)

createAccountResponse, response, err := enterpriseManagementService.CreateAccount(createAccountOptions)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(createAccountResponse, "", "  ")
fmt.Println(string(b))
```
{: codeblock}
{: go}

### Creating accounts by using Terraform
{: #create-account-terraform}
{: terraform}

Use the following steps to create accounts by using Terraform:

1. Create an argument in your `main.tf` file. The following example creates an account by using the `ibm_enterprise_account` resource, where `name` is a unique name to identify the enterprise. You must have an existing IAM ID of an enterprise primary contact in order to complete the task.

   ```terraform
   resource "ibm_enterprise_account" "enterprise_account" {
    parent = "parent"
    name = "name"
    owner_iam_id = "owner_iam_id"
    }
   ```
   {: codeblock}

   You can specify the ID of an account owner on the `owner_iam_id` option. For more information, see the argument reference details on the [Terraform Enterprise Management](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/enterprise_account){: external} page.

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}
