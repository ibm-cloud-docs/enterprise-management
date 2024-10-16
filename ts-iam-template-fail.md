---

copyright:
  years: 2021, 2023
lastupdated: "2024-10-16"

keywords: troubleshooting enterprise iam templates, iam tempalates, enterprise-managed IAM, access enteprise IAM, access templates, error message, assign template error, invalid account

subcollection: secure-enterprise

---

{{site.data.keyword.attribute-definition-list}}


# Why does my IAM template assignment fail for an account in my enterprise?
{: #iam-template-fail}
{: troubleshoot}

To successfully assign an enterprise IAM template to an account, the account must be `ACTIVE`.
{: shortdesc}

You get a the following error when assigning an IAM template to an account:
{: tsSymptoms}

> An error occurred while requesting to assign the enterprise template to some of the specified accounts or account groups. The account id, `exampleAccountID`, is invalid.

The account is `PENDING`, `CANCELED` or `SUSPENDED`. If you don't confirm a new account, the account remains in a pending state. Assigning an IAM template to a canceled account also fails.
{: tsCauses}

Check the status of the account in your enterprise.
{: tsResolve}

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Enteprrise** and click **Accounts**.
1. Click the **Table expand** icon ![Table expand icon](../icons/table-expand.svg "Table expand") on the account group where the account resides, or click on the account if it's not in a group.
1. View the status of the account. You can't assign IAM templates to `PENDING`, `CANCELED` or `SUSPENDED` accounts.
    1. If an account is `PENDING`, contact the account owner and ask them to complete their account registration. The confirmation email is sent to the email address that is associated with the owner's IBMid. If they can't find the confirmation email, they can go to the [IBM Cloud login page](https://cloud.ibm.com/){: external} and try to log in. The following message is displayed:

        > To complete your registration, check your email.
        > Can't find the email? Resend.

    1. Click Resend to send another confirmation email to the email address that is associated with your IBMid.
