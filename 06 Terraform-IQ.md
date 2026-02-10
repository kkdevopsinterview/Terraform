## 61. What is **terraform import**?

**terraform import** is a command used to bring existing
**infrastructure resources** under **Terraform management** by
associating them with **Terraform state**. In many real-world
environments, infrastructure already exists because it was created
manually through cloud consoles, scripts, or other automation tools.
When organizations decide to adopt **Infrastructure as Code**, they
don't want to destroy and recreate production resources just to manage
them with Terraform.

This is where **terraform import** plays a crucial role.

The command links an existing resource --- identified by its
provider-specific ID --- to a resource block defined in Terraform
configuration. Importing does not create or modify the infrastructure.
Instead, it updates the **Terraform state file** so Terraform begins
tracking that resource moving forward.

After importing, Terraform can:

-   Detect **configuration drift**
-   Update the resource
-   Manage lifecycle
-   Destroy it if required

However, import requires that the resource configuration already exists
in **.tf files**, because Terraform needs a destination address in state
to map the resource.

This makes **terraform import** essential when transitioning legacy
environments into Terraform-driven workflows.

### Example

``` bash
terraform import aws_instance.web i-0abc12345
```

Links an existing EC2 instance to Terraform state.

### Real-World Example

A company running production servers created manually in AWS decides to
standardize deployments using Terraform. Instead of rebuilding
everything, they import those servers so Terraform manages them safely.

### Interview Punch Lines

-   "terraform import maps existing resources into Terraform state."
-   "It enables migration from manual infrastructure to IaC."

------------------------------------------------------------------------

## 62. Why do we use **terraform import** in real infrastructure?

In real infrastructure environments, very rarely does everything start
from scratch. Enterprises often have long-running production workloads
created before Terraform adoption. Recreating these resources could
cause downtime, data loss, or operational risk.

**terraform import** enables organizations to adopt **Infrastructure as
Code gradually** without disrupting existing workloads.

It is commonly used for:

-   Modernizing legacy environments
-   Disaster recovery when state lost
-   Resource ownership transition
-   Infrastructure consolidation

Import ensures Terraform has visibility and governance over resources,
improving auditing, version control, and automation.

Without import, Terraform would treat existing resources as unknown and
might attempt duplicate creation or conflict.

### Example

Importing an existing database before applying configuration updates.

### Real-World Example

During cloud governance initiative, a company imports all networking
resources into Terraform to enforce security policies centrally.

### Interview Punch Lines

-   "Import supports gradual IaC adoption."
-   "It prevents resource duplication and disruption."

------------------------------------------------------------------------

## 63. In which scenarios is importing existing resources required?

Importing becomes necessary when infrastructure exists outside Terraform
control but needs management within Terraform workflows.

Typical scenarios include:

-   Manual console-created resources
-   Migrating from another automation tool
-   State file corruption recovery
-   Infrastructure acquisition or team handover
-   Resource restructuring into modules

In each case, import avoids destructive recreation and ensures
continuity.

Import also supports audit and compliance by allowing Terraform to track
and version infrastructure changes after onboarding.

### Example

Importing VPC and subnets before modularizing project.

### Real-World Example

A newly hired DevOps team inherits unmanaged infrastructure and imports
it to standardize deployments.

### Interview Punch Lines

-   "Import is used whenever resources pre-exist Terraform."
-   "It ensures seamless onboarding into state management."

------------------------------------------------------------------------

## 64. What happens to **Terraform state** after importing?

After import execution, Terraform updates the **state file** by
recording the association between the Terraform configuration resource
block and the actual infrastructure resource ID.

No changes occur to the infrastructure itself.

The state now includes:

-   Resource metadata
-   Attributes
-   Dependencies
-   IDs

This allows Terraform to:

-   Compare desired vs actual state
-   Generate plans
-   Perform updates

If configuration does not match real infrastructure, Terraform will
detect differences during next plan.

### Example

``` bash
terraform state list
```

Shows imported resources.

### Real-World Example

Imported load balancer appears in state and can now be scaled or
updated.

### Interview Punch Lines

-   "Import modifies state, not infrastructure."
-   "It enables lifecycle tracking."

------------------------------------------------------------------------

## 65. Does **terraform import** generate configuration automatically?

No --- Terraform does not generate configuration files automatically
during import. It only updates the **state mapping**.

This design ensures engineers explicitly define infrastructure
architecture rather than blindly accepting generated configs, which
might not follow standards or modular structure.

This encourages:

-   Proper documentation
-   Modular design
-   Version control discipline

### Real-World Example

Engineer imports database then manually writes configuration aligned
with organization standards.

### Interview Punch Lines

-   "Import updates state only."
-   "Configuration must be authored manually."

------------------------------------------------------------------------

## 66. What is **infrastructure drift** in Terraform?

Infrastructure drift refers to a situation where the actual
infrastructure running in the cloud differs from what is defined in
Terraform configuration or recorded in the Terraform state file.

Drift happens when changes occur outside Terraform's control --- such as
manual edits in the cloud console, automated scripts, or other tools
modifying resources directly.

This can lead to:

-   Unexpected resource replacement
-   Security misconfiguration
-   Cost increases
-   Compliance violations

Terraform itself doesn't prevent drift --- it detects and reports it,
allowing engineers to reconcile differences.

### Example

Manual change: Instance type changed in AWS Console

Then:

``` bash
terraform plan
```

### Interview Punch Lines

-   "Drift occurs when real infrastructure diverges from configuration."
-   "It typically results from out-of-band changes."

------------------------------------------------------------------------

## 67. How does Terraform detect **drift**?

Terraform detects drift by querying **provider APIs** during planning or
refresh operations. It compares three sources:

1 Configuration files --- desired state\
2 State file --- last known state\
3 Live infrastructure --- actual state

### Command Example

``` bash
terraform plan
```

### Interview Punch Lines

-   "Terraform queries provider APIs to detect differences."
-   "Plan operation highlights drift automatically."

------------------------------------------------------------------------

## 68. Which Terraform commands help identify drift?

Primary Command

``` bash
terraform plan
```

Additional Tools

``` bash
terraform refresh
terraform state show
```

### Interview Punch Lines

-   "terraform plan is the main drift detection tool."
-   "State inspection commands assist troubleshooting."

------------------------------------------------------------------------

## 69. What happens when drift is found during plan?

When Terraform detects drift, it presents a **proposed execution plan**
showing how to reconcile differences but takes no action automatically.

### Interview Punch Lines

-   "Terraform proposes reconciliation but takes no action."
-   "Apply required to enforce desired state."

------------------------------------------------------------------------

## 70. How should drift be handled in production?

Handling drift requires investigation:

1 Identify root cause
2 Validate change
3 Update Terraform code
4 Apply changes

Best practices:

-   Avoid manual edits
-   Enforce access control
-   Run periodic drift checks
-   Use audit logging

### Interview Punch Lines

-   "Drift must be analyzed before correction."
-   "Configuration should reflect approved reality."

------------------------------------------------------------------------

## 71. What is **terraform fmt**?

**terraform fmt** rewrites Terraform configuration into canonical style
defined by HashiCorp ensuring consistent formatting.

### Example

``` bash
terraform fmt
```

### Interview Punch Lines

-   "terraform fmt standardizes code formatting."
-   "It improves readability and collaboration."

------------------------------------------------------------------------

## 72. Why is **terraform fmt** important in teams?

Using **terraform fmt** ensures:

-   Uniform coding standards
-   Easier peer review
-   Cleaner version history
-   Automated compliance

### Interview Punch Lines

-   "Ensures consistency across contributors."
-   "Reduces review friction."

------------------------------------------------------------------------

## 73. What changes does **terraform fmt** apply?

It adjusts stylistic elements:

-   Indentation alignment
-   Argument spacing
-   Block formatting
-   Layout consistency

### Interview Punch Lines

-   "Applies style changes only."
-   "Does not modify infrastructure logic."

------------------------------------------------------------------------

## 74. What is **terraform validate**?

**terraform validate** checks Terraform configuration for **syntactic
correctness** and **internal consistency** without contacting providers.

It verifies:

-   Valid syntax
-   Correct block usage
-   Reference integrity
-   Module structure

### Example

``` bash
terraform validate
```

### Interview Punch Lines

-   "Validates configuration correctness."
-   "Prevents runtime deployment errors."
