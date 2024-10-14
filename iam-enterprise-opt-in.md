---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-14"

subcollection: secure-enterprise

keywords: enterprise, enterprise account, enable enterprise iam, turn on enterprise iam, opt in, enterprise iam, new account, existing account

---

{{site.data.keyword.attribute-definition-list}}

# Opting in to enterprise-managed IAM
{: #enterprise-managed-opt-in}

Enterprise-managed IAM centrally administers access within an enterprise by assigning preconfigured IAM resources, such as access groups, trusted profiles, and settings, to child accounts. New and existing accounts must opt-in to leverage the efficiency and enhanced security that is offered by enterprise-managed IAM.

You can sort accounts by going to **Manage > Enterprise > Accounts** and filtering on Enterprise-managed IAM.
{: tip}

## Enabling enterprise-managed IAM for existing accounts
{: #existing-acct-opt-in}
{: ui}

As the owner of a child account, you can opt in to enterprise-managed IAM by completing the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage > Account > Account settings**.
1. Go to Enterprise-managed IAM and click **On**.


## Enabling enterprise-managed IAM for new accounts
{: #new-acct-opt-in}
{: ui}

As an enterprise user with the Administrator role on the Enterprise service, you can enable enterprise-managed IAM when you create a new account. To create an account with enteprise-managed IAM enabled, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, switch to the enterprise account and go to **Manage > Enterprise**.
1. Click **Create account**.
1. **Enterprise-managed IAM** is **On** by default.
1. Click **Create**.

To disable enterprise-managed IAM in an account, the account owner must open a [support case](/unifiedsupport/supportcenter).
{: important}

## Existing accounts by using the API
{: #existing-acct-opt-in-api}
{: api}

As the owner of a child account, you can opt-in to enterprise-managed IAM. To opt-in to enterprise-managed IAM in a child account, call the [Enterprise Management API](/apidocs/enterprise-apis/enterprise) as shown in the following example:

```bash
curl -s -L -X PATCH "https://accounts.test.cloud.ibm.com/v1/accounts/$ACCOUNT/traits" \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $TOKEN" \
-d "{
    \"enterprise_iam_managed\": true
}"
```
{: codeblock}
{: curl}

## New accounts by using the API
{: #new-acct-opt-in-api}
{: api}

As an enterprise user with the Administrator role on the Enterprise service, you can enable enterprise-managed IAM when you create a new account. To create an account with enterprise-managed IAM enabled, call the [Enterprise Management API](/apidocs/enterprise-apis/enterprise#create-account) as shown in the following example:

```bash
curl -X POST "https://enterprise.cloud.ibm.com/v1/accounts -H "Authorization: Bearer <IAM_Token>" -H 'Content-Type: application/json' -d '{
  "parent": "crn:v1:bluemix:public:enterprise::a/$ENTERPRISE_ACCOUNT_ID::account-group:$ACCOUNT_GROUP_ID",
  "name": "Example Account",
  "owner_iam_id": "$OWNER_IAM_ID"
  "traits": { "enterprise_iam_managed": true }
}'
```
{: codeblock}
{: curl}

To disable enterprise-managed IAM in an account, the account owner must open a [support case](/unifiedsupport/supportcenter).
{: important}



## New accounts by using Terraform
{: #new-acct-opt-in-terra}
{: terraform}

As an enterprise user with the Administrator role on the Enterprise service, you can enable enterprise-managed IAM when you create a new account.

Before you can create an account with enterprise-managed IAM enabled by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

Complete the following steps to create an account with enterprise-managed IAM enabled:

1. In your Terraform configuration file, find the Terraform code that you used to create the enterprise and note the CRN of the parent, which can be an account group or the enterprise.
1. Create a new child account with enterprise-managed IAM enabled by including the `traits` argument with the property `enterprise_iam_managed = true`.
   ```terraform
    resource "ibm_enterprise_account" "enterprise_account" {
      parent = "parent"
      name = "name"
      owner_iam_id = "owner_iam_id"
    }

    resource "ibm_enterprise_account" "enterprise_import_account"{
      parent = "parent"
      enterprise_id = "enterprise_id"
      account_id = "account_id"
      traits {
        mfa = "NONE"
        enterprise_iam_managed = true
      }
    }
   ```
   {: codeblock}

   For more information, see the argument reference details on the [Terraform Enterprise Management](https://registry.terraform.io/providers/IBM-Cloud/ibm/1.56.0-beta0/docs/resources/enterprise_account){: external} page.

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


To disable enterprise-managed IAM in an account, the account owner must open a [support case](/unifiedsupport/supportcenter).
{: important}
