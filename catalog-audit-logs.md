---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-30"

keywords: audit log

subcollection: account

---

{{site.data.keyword.attribute-definition-list}}

# Viewing changes to your private catalogs
{: #catalog-audit-logs}

With audit logs you can follow the changes that have been made to your private catalogs. Changes to your private catalog are associated with your account or enterprise account, products, and catalog.
{: shortdesc}

To view the audit logs, you need to be a manager of the account the catalog is in, or an editor in that account and the catalog. See [Assigning access to account management services](/docs/account?topic=account-account-services) for more information.


## Viewing changes in the console
{: #audit-logs-table}
{: ui}

1. In the {{site.data.keyword.Bluemix}} console, go to **Manage** > **Catalogs** from the console menu bar.
2. Select **Audit logs**.
3. Filter for the scope you want to see in the table.

Each event in the audit logs table by default identifies each change with the email of the user that made the change, the type of change, a description of the change, and the date that the change was made.


## Viewing changes by using the CLI
{: #audit-logs-table-cli}
{: cli}

This action can be done only through the console, API, or SDKs. To see the steps, switch to the UI or API instructions.

## Viewing changes by using the API
{: #audit-logs-table-api}
{: api}

You can view changes made to your private catalogs by calling the [Catalog Management API](https://cloud.ibm.com/apidocs/resource-catalog/private-catalog#get-catalog-audit) as shown in the following sample request.

```bash
curl -X "GET" \
"https://cm.globalcatalog.cloud.ibm.com/api/v1-beta/catalogs/{catalog-id}/audit"
-H "accept: application/json"
-H "Authorization: {iam-bearer-token}"
```
{: codeblock}

Each event in the audit logs table by default identifies each change with the email of the user that made the change, the type of change, a description of the change, and the date that the change was made.

