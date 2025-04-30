---

copyright:
  years: 2018, 2025
lastupdated: "2025-04-30"

keywords:

subcollection: enterprise-management

---

{{site.data.keyword.attribute-definition-list}}



# Activity tracking events for enterprise management
{: #at_events_em}



{{site.data.keyword.cloud_notm}} services, such as enterprise management, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

## Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}

Enterprise management sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

## Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}



For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Events for managing enterprises
{: #at_events_manage_enterprise}

The following table lists the actions that generate enterprise management events:

| Action                                               | Description |
|------------------------------------------------------|-------------|
| `enterprise.enterprise.create`               | An event is generated when a user creates an enterprise. |
| `enterprise.enterprise.update`               | An event is generated when a user updates information about the enterprise. |
| `enterprise.enterprise.import`               | An event is generated when a user imports an existing stand-alone account to the enterprise hierarchy. |
| `enterprise.account-group.create`            | An event is generated when a user creates an account group within an enterprise. |
| `enterprise.account-group.update`            | An event is generated when a user updates the account group information within an enterprise. |
| `enterprise.account-group.delete`            | An event is generated when a user deletes an account group within an enterprise. |
| `enterprise.account.create`                  | An event is generated when a user creates an account within an enterprise. |
| `enterprise.account.move`                    | An event is generated when a user moves an account within an enterprise, for example, moves the account from a child account group into its parent account group. |
| `enterprise.account.update`                  | An event is generated when a user updates the account information within an enterprise. |
| `enterprise.account.delete`                  | An event is generated when a user deletes an account from an enterprise. |
{: caption="Actions that generate enterprise management events" caption-side="top"}

## Events for managing enterprise usage reports
{: #at_events_acc_mgt_reports_enterprise}

The following table lists the actions that generate an event:

| Action                                               | Description |
|------------------------------------------------------|-------------|
| `billing.enterprise-usage-report.read`               | An event is generated when a user views the enterprise account level summary usage page that is displayed by default. |
| `billing.enterprise-usage-report.download`           | An event is generated when a user requests a **summary** export of the data in csv format from the enterprise account level summary usage page.  |
| `billing.enterprise-instances-usage-report.download` | An event is generated when a user requests an **instances** export of the data in csv format from the enterprise account level summary usage page. |
{: caption="Actions that generate enterprise usage report management events" caption-side="top"}

## Analyzing enterprise billing activity tracking events
{: #at_events_iam_analyze}



### requestData fields
{: #at_events_analyze_4_reqdata}

The following table lists the fields that are available through the `requestData` field in the events with actions `billing.enterprise-usage-report.read` and `billing.enterprise-usage-report.download`:

| Field               | Type      | Description | Status |
|---------------------|-----------|-------------|--------|
| `month`             | String    | Indicates the month that the user selects to view usage data. |  Included always in the event |
| `children`          | Boolean   | Indicates whether the usage is aggregated at account level. | Included always in the event |
| `enterprise_id`     | String    | Indicates the ID of the enterprise. |  Included always in the event |
| `account_id`        | String    | Indicates the sub-account ID that is requested in the report. | Optional |
| `account_group_id`  | String    | Indicates the account group when a user selects one. | Optional   \n Included if the user filters data by selecting 1 account group. |
{: caption="Enterprise usage requestData fields" caption-side="top"}

The following table lists the fields that are available through the `requestData` field in the events with actions `billing.enterprise-instances-usage-report.download`:

| Field               | Type      | Description | Status |
|---------------------|-----------|-------------|--------|
| `month`             | String    | Indicates the month that the user selects to view usage data. |  Included always in the event |
| `enterprise_id`     | String    | Indicates the ID of the enterprise. |  Included always in the event |
| `account_id`        | String    | Indicates the sub-account IDs that are requested in the report. | Optional |
| `account_group_id`  | String    | Indicates the account group when a user selects one. | Optional   \n Included if the user filters data by selecting 1 account group. |
{: caption="Enterprise instances usage requestData fields" caption-side="top"}
