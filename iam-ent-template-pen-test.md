---

copyright:
  years: 2023. 2025
lastupdated: "2025-02-18"

keywords: enterprise, enterprise account, multiple accounts, assign access, enterprise access, templates, enterprise managed, access, enterprise trusted profile, penetration testing

subcollection: enterprise-management

content-type: tutorial
account-plan: paid
completion-time: 15m

---

{{site.data.keyword.attribute-definition-list}}

# Centrally managing access for external security consultants in an enterprise
{: #enterprise-iam-tp-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="15m"}

This tutorial walks you through setting up a trusted profile template that grants a team of external security consultants access to child accounts in your enterprise. This way, they can complete various types of tests, such as network penetration testing, web application testing, and cloud-specific assessments.
{: shortdesc}

A combination of internal and external security professionals typically do penetration testing for a multi-account cloud environment. Enterprises often engage with external penetration testing firms with expertise in cloud security to do independent assessments.

Many organizations do penetration tests on a regular schedule, such as quarterly, semiannually, or annually. Routine testing helps make sure that security controls are continuously assessed and improved. Based on your schedule, you can give an external testing team the access that they need, only when they need it, by creating trusted profile templates with time-based policies.

The tutorial uses a fictitious company that is called *Example Corp*, which wants to create a trusted profile template for an external testing team in an enterprise with the following structure. As you complete the tutorial, adapt each step to match your organization's accounts and structure.

![A four-tier enterprise that groups accounts according to department in an organization. For example, account groups are named Marketing, Development, and Sales. The account groups contain accounts for teams within those departments. For example, the Sales account group contains accounts for Direct, Online, and Enablement.](images/enterprise-by-dept.svg "An enterprise that organizes accounts according to department in the organization."){: caption="Figure 1. An enterprise that is organized by department" caption-side="bottom"}


## Before you begin
{: #before-ent-iam-tutorial}

- Check out [Best practices for assigning access in an enterprise](/docs/enterprise-management?topic=enterprise-management-access-enterprises) to learn more about the features, concepts, and components of the enterprise-managed access system.

- Verify that you're in the root enterprise account by going to **Manage** > **Enterprise** in the {{site.data.keyword.cloud_notm}} console.

- Verify that you're assigned the following {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) roles:
    * Template Administrator on All IAM Account Management services
    * Template Assignment Administrator on All IAM Account Management services
    * Viewer role on the Enterprise service

- Make sure that you enable authentication from an external identity provider by using IBMid federation to register your company's domain. For more information, see the [IBMid Enterprise Federation Adoption Guide](https://www.ibm.com/docs/en/ief){: external}.

   Use IBMid federation to connect the external identity provider to your enterprise. Then, you can create the trusted profile template so that the security consultants can authenticate to {{site.data.keyword.cloud_notm}} seamlessly.
   {: note}

## Create the trusted profile template
{: #tp-template}
{: step}

A trusted profile template establishes consistent access for federated users across your multi-account cloud environment. It is a predefined set of permissions and policies that you can assign consistently across multiple accounts for a specific group of users without adding them to the accounts.

Trusted profile templates reduce policy drift in common trusted profiles in your enterprise.
{: tip}

To create a trusted profile template for external security consultants, complete the following steps:

1. Go to **Manage** > **Access (IAM)** > **Enterprise** > **Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Click **Trusted profiles** and click **Create**.
1. Name the trusted profile template "External security template".
1. Enter a description such as "External security team needs read access to Kubernetes and VPC to conduct PEN testing."

   The template name and description are shown only in your enterprise account.
   {: note}

1. Name the trusted profile "External security profile".
1. Enter a description such as "External security team has Read access to Kubernetes and VPC to conduct PEN testing."

   The trusted profile name and description are shown to users that can apply the profile when they log in. They are also visible to all users in the account where the profile is assigned.
   {: note}

1. Click **Create**.

After the trusted profile template is created, you are directed to the template dashboard. From here, you can view the template details and customize the template for the external security consultants.


## Add the trust relationship
{: #trust-template}
{: step}

Establish trust between your cloud environment and the external penetration testing team. Create conditions based on the SAML attributes from their IdP to determine which users from their directory can apply the trusted profile. For more information, see [Using IdP data to build trusted profiles](/docs/account?topic=account-idp-integration#trusted-profiles-idp-data).

1. Click the **Trust relationship** tab and click **Add**.
1. Select the authentication method **Users federated by IBMid**.
1. Select the IdP that you connected.
1. Click **Add a condition**.
   1. Allow users when `group` contains `ibm_compliance_consultant`.

   `group` is an example IdP attribute that is assigned to the external users in their own corporate directory. This condition identifies the team of security consultants that work with {{site.data.keyword.IBM_notm}} to do penetration testing. Adapt the attributes and values to match your organization's situation.
   {: note}

1. Set the session duration to 8 hours. Access is revoked after this time period expires, and users must log back in.
1. Click **Save**.

## Define the access
{: #tp-access}
{: step}

Define the set of roles that external security consultants can use in child accounts that you select. Complete the following steps to add an access policy to your trusted profile template:

1. Within the trusted profile template, click **Access**. 
1. Click **Add**.
1. Click **Create**. 
   1. Name the policy "VPC PEN testing".

      Name your policies to clearly indicate their purpose.
      {: note}

   1. Enter the description "Read access on VPC services for external penetration testing", and click **Next**.
   1. Select **VPC Infrastructure Services** and click **Next**.
   1. Select **All resources** > **Next**.
   1. Select the **Viewer** role and click **Next**. This way the security consultants can do things like list virtual storage machines, see resource groups, and view the details of a flow log collector. 
   1. Click **Add condition** to schedule a time-based policy that grants access only during the annual audit.
   1. Click **Schedule** > **Next**.
   1. Select the time zone UTC-4, the East Coast of the United States.
   1. Select the start date and time, 2025-02-18.
   1. Select the end date and time, 2025-03-18.

   After the end date and time, the policy no longer grants access.
   {: note}

   1. Click **Create**. 
   1. Click **Add**. 
   1. Go to **Access**.
1. Click **Create** to add another policy.
   1. Name the policy "Kubernetes PEN testing".

      Name your policies to clearly indicate their purpose.
      {: note}

   1. Enter the description "Read access on Kubernetes clusters for external penetration testing", and click **Next**.
   1. Select **Kubernetes service** > **Next**.
   1. Select **All resources** > **Next**.
   1. Select the **Viewer** role. This way the security consultants can view cluster details but not modify the infrastructure.
   1. Click **Add**.

   The Kubernetes service doesn't support time-based policies.
   {: note}

Security consultants need these policies to view clusters, cluster IPs, and compute resources. By viewing clusters and cluster IPs, consultants can assess the network architecture and configurations, including how different clusters are interconnected. This is crucial for identifying network-level vulnerabilities, like exposed ports, insecure network policies, or improper segmentation.

In penetration testing, consultants simulate cyberattacks to discover vulnerabilities and assess the security posture. Access to clusters and compute resources is often necessary to do penetration tests, as it allows them to simulate attacks on containerized applications, container orchestrators, or cloud services.

Make sure that Access for external security consultants is temporary and monitored. For more information, see [Monitoring enterprise IAM templates](/docs/enterprise-management?topic=enterprise-management-monitor-enterprise-iam-templates).
{: tip}

## Review and commit your trusted profile template
{: #tp-review}
{: step}

Committing a template makes it immutable, meaning that you can't change its configuration when it's committed. The commitment step makes sure that the access that is defined at the enterprise level remains consistent and secure. Any new changes require a new version, which is managed intentionally.

1. Click **Review**. Take a minute to review the details of the trusted profile template. Committing a template can't be undone, so make sure that everything is correct.
1. Click the checkbox to confirm that you understand the impact of committing your template.
1. Click **Commit**.

After you commit the template, the Template Assignment Administrator can assign the trusted profile template to the child accounts where the security consultants need access.

## Assign your trusted profile template to child accounts
{: #tp-assign}
{: step}

When you assign the trusted profile template to child accounts, an instance of the trusted profile is created in each account. To assign a trusted profile template to child accounts, complete the following steps:

1. Click **Assign accounts**.
1. Select the accounts where compliance officers need access. For *Example Corp*, compliance officers need access in the entire Development account group, the Sales account group, and the Marketing account group.

   Selecting an account group assigns the trusted profile template to all accounts in the group, any accounts moved into the group, or new accounts created in the group.
   {: note}

1. Click **Assign accounts**.

After the trusted profile template is assigned, you are directed to the Assignment reports. From here, you can view the assignment details and manage where the template is assigned. When the trusted profile template is successfully assigned to an account, the security consultants can access those accounts by applying the trusted profile.

## Manage the lifecycle of your trusted profile template
{: #tp-lifecycle}
{: step}

After the external security consultants finish their annual audit, remove the trusted profile assignment from all child accounts. Removing the assignments disables their access to accounts in your enterprise.

1. Go to **Manage** > **Access (IAM)** > **Enterprise** > **Templates** in the {{site.data.keyword.cloud_notm}} console.
1. Click the **Trusted profiles** tab.
1. Click the trusted profile template "External security template".
1. Click **Assignments**.
1. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Remove** for the Development account group.
1. Confirm that you want to remove the assignment by clicking **Remove**.
1. Repeat these steps for the Sales account group and the Marketing account group.

When the external security consultants need access again next year, you can create another version of the template and update the time-based policy to grant access for the correct dates.
