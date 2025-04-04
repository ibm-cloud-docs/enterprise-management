---
copyright:
 years: 2025
lastupdated: "2025-04-04"

keywords: enterprise, enterprise account, multiple accounts, assign access, enterprise access, templates, enterprise managed, access, enterprise access group

subcollection: enterprise-management

content-type: tutorial
completion-time: 15m

---
{{site.data.keyword.attribute-definition-list}}

# Centrally managing resources in an enterprise account by using APIs
{: #enterprise-manage-resource-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="15m"}

A common request from companies across many industries is how to manage cloud resources across their accounts centrally. At {{site.data.keyword.cloud}}, there are a few ways to complete this task. You can either use [{{site.data.keyword.cloud_notm}} projects to manage the Infrastructure as code (IaC)](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects), or you can use an API directly, which is recommended for companies with existing resource management systems that are looking to extend them to include {{site.data.keyword.cloud_notm}} resources. This tutorial walks you through the steps on using a single service ID to manage resources in all enterprise subaccounts by using only API requests. Steps 1–5 are one-time configuration steps that are required to set up access and permissions, while steps 6–9 are operational steps that must be performed each time you want to manage account resources. The configuration steps include obtaining access credentials, creating the necessary service identities, and defining access policies. The operational steps involve retrieving access tokens, listing the trusted profiles that the operator service ID can use, generating an access token for the child account, and using them to manage resources.
{: shortdesc}

Resource management can be automated for child accounts that use a [service ID](/docs/account?topic=account-serviceids&interface=ui) and [enterprise-managed {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) templates](https://www.ibm.com/new/announcements/introducing-ibm-cloud-enterprise-managed-iam){: external} from the enterprise root account. First, you must have a service ID and an API key, which can be from the enterprise root account, or from any other existing child account in the enterprise. Then, you can use the trusted profile and access policy templates to assign the required access for managing resources. Next, the templates can be assigned to the child accounts in the enterprise you want to manage. Finally, by using the assigned trusted profiles and the service ID’s API key, you can manage resources in the context of each child account.

## Before you begin
{: #prereqs-ent-manage-resource}

* Create a service ID and an API key specific to the service ID. This is your operations service ID that is used to manage resources in the child accounts. For more information, see [Creating and working with service IDs](/docs/account?topic=account-serviceids&interface=ui).
* Have user or service ID credentials with access to create and assign IAM templates `Viewer` role on the **Enterprise** service. This user or service ID must be different than the operations service ID and it is needed only once to complete the set up.
* Verify that you're assigned the following IAM roles:
    * Template administrator on **All IAM Account Management services**
    * Template assignment administrator on **All IAM Account Management services**
* Enable the enterprise-managed IAM setting for the enterprise child account. For more information, see [Opting in to enterprise-managed IAM](/docs/enterprise-management?topic=enterprise-management-enterprise-managed-opt-in&interface=ui).

## Obtain an access token
{: #get-access-token}
{: step}

To create and assign the enterprise IAM templates, you must obtain an access token first. The access token represents the user or other identity with access to manage service IDs and IAM templates. You can obtain an access token by using either the API or the CLI.

The following example shows how to obtain a token by using the API:

```bash
curl -X POST "https://iam.cloud.ibm.com/identity/token" \
--header "Content-Type: application/x-www-form-urlencoded" \
--data 'grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=$MY_APIKEY'
{
  "access_token": "reallylong.token.here",
  "refresh_token": "not_supported",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1727978763,
  "scope": "ibm openid"
}
```
{: codeblock}

The following example shows how to obtain a token by using the CLI:

1. Log in to {{site.data.keyword.cloud_notm}}:

   ```bash
   ibmcloud login
   ```
   {: codeblock}

1. Obtain the access token:

   ```shell
   $ ibmcloud iam oauth-tokens
   IAM token:  Bearer reallylong.token.here
   ```
   {: codeblock}

## (Optional) Create the operations service ID and API key in the enterprise account
{: #create-service-id}
{: step}

You can skip this step if you already have a service ID and an associated API key created.
{: note}

By using the obtained access token from the previous step, create a service ID by calling the [IAM Identity Services API](/apidocs/iam-identity-token-api#create-service-id) as shown in the following example:

```bash
curl -X POST "https://iam.cloud.ibm.com/v1/serviceids" \
--header "Authorization: Bearer <TOKEN>" \
--header "Content-Type: application/json" \
--data '{
    "name": "Operator resource manager identity",
    "description": "Operator service id to manage resources in child accounts",
    "account_id": "<ACCOUNT_ID>"
}'
```
{: codeblock}
{: curl}

See the following sample response:

```json
{
  "id": "ServiceId-cb36c9a9-778f-4985-a398-dbec6523054a",   
  "iam_id": "iam-ServiceId-cb36c9a9-778f-4985-a398-dbec6523054a",
  "entity_tag": "1-b5edc4362f94fb1fa5f009467b1db039",
  "crn": "crn:v1:bluemix:public:iam-identity::a/ACCOUNT_ID::serviceid:ServiceId-cb36c9a9-778f-4985-a398-dbec6523054a",
  "locked": false,
  "created_at": "2024-10-04T14:05+0000",
  "modified_at": "2024-10-04T14:05+0000",
  "account_id": "ACCOUNT_ID",
  "name": "Operator resource manager identity",
  "description": "Operator service id to manage resources in child accounts",
  "unique_instance_crns": []
}
```
{: codeblock}

Then, you can create the service ID’s API key by calling the [IAM Identity Services API](/apidocs/iam-identity-token-api#create-api-key) as shown in the following example:

```bash
curl -X POST "https://iam.cloud.ibm.com/v1/apikeys"\
--header "Authorization: Bearer <TOKEN>"\
--header "Content-Type: application/json"\
--data '{
    "name": "Operator resource manager apikey",
    "description": "Operator key to manage resources in child accounts",
    "iam_id": "ServiceId-cb36c9a9-778f-4985-a398-dbec6523054a",
    "account_id": "<ACCOUNT_ID>",
    "store_value": false
}'
```
{: codeblock}
{: curl}

See the following sample response:

```json
{
  "id": "ApiKey-5ccff000-9ff1-4481-a760-29c22a7603e7",
  "entity_tag": "1-b4053b5d441613fdad4ff3c28db3e7cc",
  "crn": "crn:v1:bluemix:public:iam-identity::a/ACCOUNT_ID::apikey:ApiKey-5ccff000-9ff1-4481-a760-29c22a7603e7",
  "locked": false,
  "disabled": false,
  "created_at": "2024-10-04T12:28+0000",
  "created_by": "IBMid-110000AB1Z",
  "modified_at": "2024-10-04T12:28+0000",
  "support_sessions": false,
  "action_when_leaked": "none",
  "name": "Operator resource manager apikey",
  "description": "Operator key to manage resources in child accounts",
  "iam_id": "ServiceId-cb36c9a9-778f-4985-a398-dbec6523054a",
  "account_id": "ACCOUNT_ID",
  "apikey": "created_apikey"
}
```
{: codeblock}

## Create the access policy templates
{: #create-policy-templates}
{: step}

Now, you can create two access policy templates to grant the required access to manage all services. These templates are used in the next step to grant access to the trusted profile.

Create the templates to grant the required access to manage all services by calling the [IAM Identity Services API](/apidocs/iam-policy-management#create-policy-template) as shown in the following example:

You must assign the `Administrator` role for all catalog services.
{: important}

```bash
curl --location 'https://iam.cloud.ibm.com/v1/policy_templates' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
--data '{
  "name": "ServiceAdministrator",
  "description": "Manage services",
  "account_id": "<ACCOUNT_ID>",
  "committed": true,
  "policy": {
    "type": "access",
    "description": "Manage all services",
    "resource": {
      "attributes": [
        {
          "key": "serviceType",
          "operator": "stringEquals",
          "value": "service"
        }
      ]
    },
    "control": {
      "grant": {
        "roles": [{
          "role_id": "crn:v1:bluemix:public:iam::::role:Administrator"
        }]
      }
    }
  }
}'
```
{: codeblock}
{: curl}

See the following sample response:

```json
{
  "id": "policyTemplate-8e27d6d9-4e9c-4cfd-a431-15d2010a7f82",
  "name": "ServiceAdministrator",
  "account_id": "ACCOUNT_ID",
  "description": "Manage services",
  "version": "1",
  "policy": {
    "type": "access",
    "description": "Manage all services",
    "resource": {
      "attributes": [
        {
          "key": "serviceType",
          "operator": "stringEquals",
          "value": "service"
        }
      ]
    },
    "control": {
      "grant": {
        "roles": [
          {
            "role_id": "crn:v1:bluemix:public:iam::::role:Administrator"
          }
        ]
      }
    }
  },
  "created_at": "2024-10-03T17:22:09.004Z",
  "created_by_id": "iam-ServiceId-66306ad9-5fe6-472e-94bc-ad73c33352ca",
  "last_modified_at": "2024-10-03T17:22:09.004Z",
  "last_modified_by_id": "iam-ServiceId-66306ad9-5fe6-472e-94bc-ad73c33352ca",
  "counts": {
    "template": {
      "current": 27,
      "limit": 100
    },
    "version": {
      "current": 1,
      "limit": 100
    }
  },
  "href": "https://iam.test.cloud.ibm.com/v1/policy_templates/policyTemplate-8e27d6d9-4e9c-4cfd-a431-15d2010a7f82",
  "state": "active",
  "committed": true
}
```
{: codeblock}

Create an access policy template to grant the access required to manage resource groups:

```bash
curl --location 'https://iam.cloud.ibm.com/v1/policy_templates' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <TOKEN>' \
--data '{
  "name": "ResourceGroupAdministrator",
  "description": "Resource Group Administrator",
  "account_id": "<ACCOUNT_ID>",
  "committed": true,
  "policy": {
    "type": "access",
    "description": "Manage all Resource Groups",
    "resource": {
      "attributes": [
        {
          "key": "resourceType",
          "operator": "stringEquals",
          "value": "resource-group"
        }
      ]
    },
    "control": {
      "grant": {
        "roles": [{
          "role_id": "crn:v1:bluemix:public:iam::::role:Administrator"
        }]
      }
    }
  }
}'
```
{: codeblock}
{: curl}

## Create the trusted profile template
{: #create-tp-template-ent-tutorial}
{: step}

Create the trusted profile template with the operator service ID as the trusted entity and the two policy templates from the [Create the access policy templates](#create-policy-templates) step by calling the [IAM Identity Services API](/apidocs/iam-identity-token-api#create-profile-template) as shown in the following example:

```bash
curl -X POST "https://iam.cloud.ibm.com/v1/profile_templates" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer <TOKEN>" \
--data '{
    "account_id": "<ENTERPRISE_ACCOUNT_ID>",
    "name": "Resource Manager template",
    "commited": true,
    "profile": {
        "name": "Profile for Service Adminstrator",
        "description": "Manage all services in the account",
        "identities": [
            {
                "type": "serviceid",
                "identifier": "<enter the service id like: ServiceId-123456789>"
            }
        ]
    },
    "policy_template_references": [
        {
            "id": "<Service Administrator policy template id>",
            "version": 1
        },
        {
            "id": "<Resource Group Administrator policy template id>",
            "version": 1
        },
    ]
}'
```
{: codeblock}
{: curl}

## Assign the trusted profile template to an account group
{: #assign-tp-template}
{: step}

The template can be assigned to individual accounts or account groups (recommended). When you assign a template to an account group, a trusted profile gets created in each child account in the account group. Also, the system automatically creates trusted profiles for new accounts that are added to the account group, or removes them when child accounts are removed or deleted from the group. Create an assignment for a trusted profile template by calling the [IAM Identity Services API](/apidocs/iam-identity-token-api#create-trusted-profile-assignment) as shown in the following example:

```bash
curl -X POST "https://iam.cloud.ibm.com/v1/profile_assignments"\
--header "Content-Type: application/json"\
--header "Authorization: Bearer <TOKEN>"\
--data '{
    "template_id": "<Trusted Profile template id>",
    "template_version": 1,
    "target_type": "AccountGroup",
    "target": "<account group id>"
}'
```
{: codeblock}
{: curl}

## Get the service ID’s access token
{: #get-serviceid-token}
{: step}

To manage the enterprise account resources, you must use the operations service ID's API key that you created previously to obtain an access token. Call the [IAM Identity Services API](/apidocs/iam-identity-token-api#gettoken-apikey) as shown in the following example:

```bash
curl -X POST "https://iam.cloud.ibm.com/identity/token" \
--header "Content-Type: application/x-www-form-urlencoded" \
--data 'grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=<OPERATOR_APIKEY>'
```
{: codeblock}
{: curl}

See the following sample response:

```json
{
  "access_token": "reallylong.token.here",
  "refresh_token": "not_supported",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1727978763,
  "scope": "ibm openid"
}
```
{: codeblock}

## Get a list of trusted profiles for the service ID
{: #get-list-tp}
{: step}

By calling the [IAM Identity Services API](/apidocs/iam-identity-token-api) as shown in the following example, you can return the list of trusted profiles and accounts that the operator service ID can use:

```bash
curl --location 'https://iam.cloud.ibm.com/identity/profiles' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'access_token=<service id token>'
```
{: codeblock}
{: curl}

See the following sample response:

```json
{
  "count": 5,
  "profiles": [
    {
      "id": "Profile-6e1f7ea6-734c-49f5-832a-cd8f4aaed739",
      "entity_tag": "2-b36be9d5a3152ef753a76c0baf4293f2",
      "crn": "crn:v1:staging:public:iam-identity::a/6e42a47f8ae143fa9accc55dfe22096f::profile:Profile-6e1f7ea6-734c-49f5-832a-cd8f4aaed739",
      "name": "Access Report",
      "description": "read only access to reports",
      "created_at": "2024-04-12T19:00+0000",
      "modified_at": "2024-04-12T19:30+0000",
      "iam_id": "iam-Profile-6e1f7ea6-734c-49f5-832a-cd8f4aaed739",
      "account_id": "6e42a47f8ae143fa9accc55dfe22096f",
      "template_id": "ProfileTemplate-69178281-39e6-46b3-ad3f-53735a3f9282",
      "assignment_id": "TemplateAssignment-2498765a-86f4-4093-8e70-7f7f06182669"
    },
    {
      "id": "Profile-9f6c71c2-6fab-4e5e-a47c-bdf00ef350da",
      "entity_tag": "2-2586919946891dc9ec5e4e3ebf1a6ed4",
      "crn": "crn:v1:staging:public:iam-identity::a/5dd10bd7e9a44ac990813d234649a752::profile:Profile-9f6c71c2-6fab-4e5e-a47c-bdf00ef350da",
      "name": "Access Report",
      "description": "read only access to reports",
      "created_at": "2024-04-12T19:00+0000",
      "modified_at": "2024-04-12T19:30+0000",
      "iam_id": "iam-Profile-9f6c71c2-6fab-4e5e-a47c-bdf00ef350da",
      "account_id": "5dd10bd7e9a44ac990813d234649a752",
      "template_id": "ProfileTemplate-69178281-39e6-46b3-ad3f-53735a3f9282",
      "assignment_id": "TemplateAssignment-2498765a-86f4-4093-8e70-7f7f06182669"
    },
    {
      "id": "Profile-d99e8cf3-da65-42ec-94ed-fcf72f186e1e",
      "entity_tag": "2-9e5c3cd8b1d13ab26d528e4d52183954",
      "crn": "crn:v1:staging:public:iam-identity::a/8c2f25994fb74fe18539205580885559::profile:Profile-d99e8cf3-da65-42ec-94ed-fcf72f186e1e",
      "name": "Access Report",
      "description": "read only access to reports",
      "created_at": "2024-04-12T19:00+0000",
      "modified_at": "2024-04-12T19:30+0000",
      "iam_id": "iam-Profile-d99e8cf3-da65-42ec-94ed-fcf72f186e1e",
      "account_id": "8c2f25994fb74fe18539205580885559",
      "template_id": "ProfileTemplate-69178281-39e6-46b3-ad3f-53735a3f9282",
      "assignment_id": "TemplateAssignment-2498765a-86f4-4093-8e70-7f7f06182669"
    },
    {
      "id": "Profile-2cbc3b11-ef06-4d90-8709-68a758fe4cd0",
      "entity_tag": "2-ed21407aa67df82b58987c265d54b270",
      "crn": "crn:v1:staging:public:iam-identity::a/948ee4a53bfd435f8b8c195e08f2bbac::profile:Profile-2cbc3b11-ef06-4d90-8709-68a758fe4cd0",
      "name": "Access Report",
      "description": "read only access to reports",
      "created_at": "2024-04-12T19:00+0000",
      "modified_at": "2024-04-12T19:30+0000",
      "iam_id": "iam-Profile-2cbc3b11-ef06-4d90-8709-68a758fe4cd0",
      "account_id": "948ee4a53bfd435f8b8c195e08f2bbac",
      "template_id": "ProfileTemplate-69178281-39e6-46b3-ad3f-53735a3f9282",
      "assignment_id": "TemplateAssignment-2498765a-86f4-4093-8e70-7f7f06182669"
    },
    {
      "id": "Profile-5ec4f299-bb24-4867-a254-120788e64b47",
      "entity_tag": "2-2c47981665dc44c265008baece9e4ea6",
      "crn": "crn:v1:staging:public:iam-identity::a/002f345a049b4f11ae6206661e5cb438::profile:Profile-5ec4f299-bb24-4867-a254-120788e64b47",
      "name": "Access Report",
      "description": "read only access to reports",
      "created_at": "2024-04-12T19:00+0000",
      "modified_at": "2024-04-12T19:30+0000",
      "iam_id": "iam-Profile-5ec4f299-bb24-4867-a254-120788e64b47",
      "account_id": "002f345a049b4f11ae6206661e5cb438",
      "template_id": "ProfileTemplate-69178281-39e6-46b3-ad3f-53735a3f9282",
      "assignment_id": "TemplateAssignment-2498765a-86f4-4093-8e70-7f7f06182669"
    }
  ]
}
```
{: codeblock}

## Create an access token for the child account's trusted profile
{: #get-child-tp-token}
{: step}

By using the operations service ID's access token, each trusted profile ID and the ID of the child account, you can create an access token for a trusted profile. Call the [IAM Identity Services API](/apidocs/iam-identity-token-api#gettoken-assume) as shown in the following example:

```bash
curl -X POST "https://iam.cloud.ibm.com/identity/token"\
  --header "Content-Type: application/x-www-form-urlencoded"\
  --data-urlencode 'grant_type=urn:ibm:params:oauth:grant-type:assume'\
  --data-urlencode 'access_token=<ACCESS-TOKEN>'\
  --data-urlencode 'profile_id=<Profile-5ec4f299-bb24-4867-a254-120788e64b47>'
```
{: codeblock}
{: curl}

## Use the trusted profile token to manage resources in the child account
{: #use-TP-manage-resources}
{: step}

Now, you can make requests to resource APIs, for example creating a new {{site.data.keyword.cloudant_short_notm}} instance within an account by calling the [Resource Controller API](/apidocs/resource-controller/resource-controller#create-resource-instance) as shown in the following example:

```bash
curl -X POST https://resource-controller.cloud.ibm.com/v2/resource_instances -H "Authorization: Bearer <IAM token>" -H 'Content-Type: application/json' -d '{
    "name": "my-instance",
    "target": "us-south",
    "resource_group": "5c49eabc-f5e8-5881-a37e-2d100a33b3df",
    "resource_plan_id": "cloudant-standard",
    "tags": [
      "my-tag"
    ]
  }'
```
{: codeblock}
{: curl}

