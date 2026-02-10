## 46. What is **count** in Terraform?

**count** is a **meta-argument** in Terraform used to create multiple
instances of a resource using a numeric value. Instead of writing the
same resource block multiple times, we specify how many copies Terraform
should create, and Terraform assigns each instance an **index starting
from zero**.

This index can be accessed using **count.index**, which allows dynamic
naming or configuration per instance.

count is useful when:

-   Resources are identical
-   Quantity is fixed
-   No unique identity required

However, it tracks resources by index, meaning if ordering changes,
Terraform may recreate resources unintentionally.

### Example

``` hcl
resource "aws_instance" "server" {
  count = 3

  ami           = "ami-0abc123"
  instance_type = "t2.micro"

  tags = {
    Name = "server-${count.index}"
  }
}
```

### Output

    server-0
    server-1
    server-2

### Real-World Example

Creating three identical web servers for a staging environment without
writing three blocks.

### Interview Punch Lines

-   "count creates multiple resource copies using numeric indexing."
-   "It reduces code duplication for identical infrastructure."

------------------------------------------------------------------------

## 47. Why do we use **count** in resource creation?

count simplifies infrastructure scaling and avoids repetitive
configuration. It enables dynamic resource creation based on variables
or conditions, improving maintainability and automation.

It supports:

-   Quick scaling
-   Conditional resources
-   Simplified configuration

### Example --- Conditional Creation

``` hcl
resource "aws_instance" "server" {
  count = var.create ? 1 : 0
}
```

### Real-World Example

Creating extra instances only in production environment using
variable-driven logic.

### Interview Punch Lines

-   "count enables scalable and conditional provisioning."
-   "It keeps Terraform code clean and reusable."

------------------------------------------------------------------------

## 48. What is **for_each** in Terraform?

for_each is used to create multiple resources by iterating over
collections like lists, sets, or maps. Each resource gets a unique key
identity instead of numeric indexing, making tracking stable.

This prevents resource recreation when list ordering changes.

### Example

``` hcl
variable "names" {
  default = ["dev", "test", "prod"]
}

resource "aws_instance" "server" {
  for_each = toset(var.names)

  tags = {
    Name = each.key
  }
}
```

### Real-World Example

Deploying instances named after environments with distinct identities.

### Interview Punch Lines

-   "for_each creates resources using key-based identity."
-   "It provides safer lifecycle management."

------------------------------------------------------------------------

## 49. How does **for_each** work with lists and maps?

## KK FUNDA
With lists/sets: - Each item becomes a key - Access via each.key

With maps: - Keys and values used directly - Access via each.key and
each.value

Maps allow richer configuration per resource.

### Example --- Map

``` hcl
variable "servers" {
  default = {
    dev  = "t2.micro"
    prod = "t2.large"
  }
}

resource "aws_instance" "server" {
  for_each      = var.servers
  instance_type = each.value
}
```

### Real-World Example

Provisioning different instance sizes per environment.

### Interview Punch Lines

-   "for_each supports structured provisioning."
-   "Maps allow unique configurations."

------------------------------------------------------------------------

## 50. Difference between **count** and **for_each**

count tracks resources by index, making it sensitive to order changes.
for_each tracks by key identity, providing stability and safer updates.

  Feature              count     for_each
  -------------------- --------- -----------
  Identity             Index     Key
  Stability            Low       High
  Config flexibility   Limited   High
  Production use       Rare      Preferred

### Real-World Example

Removing one item causes recreation with count, but minimal change with
for_each.

### Interview Punch Lines

-   "count is index-based, for_each is key-based."
-   "for_each is safer for production."

------------------------------------------------------------------------

## 51. When should **count** be avoided in Terraform projects?

count should be avoided when resource identity and stability are
important. Terraform tracks resources created with count using numeric
indexes. If the list or number changes indexes shift and Terraform may
destroy and recreate resources unintentionally.

This becomes dangerous in production environments because recreation can
cause downtime, data loss, or service disruption.

Avoid count when: - Resources have unique names - Order may change -
Infrastructure is critical - Frequent additions/removals expected

### Example Showing the Problem

``` hcl
variable "servers" {
  default = ["web", "api", "db"]
}

resource "aws_instance" "server" {
  count = length(var.servers)
}
```

### Real-World Example

Using count to manage production database nodes causing outage when
entries change.

### Interview Punch Lines

-   "Avoid count when resource identity matters."
-   "Index shifting can cause unintended recreation."

------------------------------------------------------------------------

## 52. When is **for_each** preferred over count?

for_each is preferred when resources need stable identification or
unique configuration. Terraform tracks resources using keys so adding or
removing items does not affect others.

Ideal for: - Production workloads - Named resources - Maps or structured
data - Frequent changes

### Example

``` hcl
variable "servers" {
  default = {
    web = "t2.micro"
    db  = "t2.large"
  }
}

resource "aws_instance" "server" {
  for_each      = var.servers
  instance_type = each.value
}
```

### Real-World Example

Managing multiple subnets or storage buckets with different settings.

### Interview Punch Lines

-   "for_each ensures stable resource tracking."
-   "Preferred for production and unique configs."

------------------------------------------------------------------------

## 53. What is **depends_on** in Terraform?

depends_on explicitly tells Terraform that one resource must be created
before another.

### Example

``` hcl
resource "aws_security_group" "sg" {
  name = "web-sg"
}

resource "aws_instance" "server" {
  ami           = "ami-xyz"
  instance_type = "t2.micro"

  depends_on = [aws_security_group.sg]
}
```

### Real-World Example

Ensuring IAM roles or logging exist before compute instances.

### Interview Punch Lines

-   "depends_on enforces execution order."
-   "It resolves hidden dependencies."

------------------------------------------------------------------------

## 54. Why is explicit dependency required sometimes?

Terraform dependency graph runs resources in parallel when no references
exist. Explicit dependency ensures proper orchestration when timing
matters.

### Example

``` hcl
resource "null_resource" "setup" {}

resource "aws_instance" "server" {
  depends_on = [null_resource.setup]
}
```

### Real-World Example

Running configuration scripts before provisioning servers.

### Interview Punch Lines

-   "Prevents race conditions."
-   "Ensures proper orchestration."

------------------------------------------------------------------------

## 55. What are **lifecycle rules** in Terraform?

Lifecycle rules customize resource management behavior.

Common settings: - prevent_destroy - create_before_destroy -
ignore_changes

### Example

``` hcl
resource "aws_instance" "server" {
  lifecycle {
    create_before_destroy = true
  }
}
```

### Real-World Example

Maintaining uptime during upgrades.

### Interview Punch Lines

-   "Lifecycle controls resource behavior."
-   "Used for safety and availability."

------------------------------------------------------------------------

## 56. Where is lifecycle block defined?

Inside a resource block affecting only that resource.

### Example

``` hcl
resource "aws_db_instance" "db" {
  lifecycle {
    prevent_destroy = true
  }
}
```

### Real-World Example

Applying deletion protection to database resources.

### Interview Punch Lines

-   "Lifecycle is resource-specific."
-   "Configured inside resource definition."

------------------------------------------------------------------------

## 57. What is **prevent_destroy**?

Prevents Terraform from deleting resource even if configuration requires
it.

### Example

``` hcl
lifecycle {
  prevent_destroy = true
}
```

### Real-World Example

Protecting customer data database.

### Interview Punch Lines

-   "Acts as deletion safety lock."
-   "Used for critical resources."

------------------------------------------------------------------------

## 58. What is **create_before_destroy**?

Ensures replacement resource created before existing one destroyed.

### Example

``` hcl
lifecycle {
  create_before_destroy = true
}
```

### Real-World Example

Replacing application servers during upgrade.

### Interview Punch Lines

-   "Supports zero downtime deployments."
-   "Maintains availability."

------------------------------------------------------------------------

## 59. How does it prevent downtime?

Terraform provisions new resource shifts dependencies then deletes old
one.

### Real-World Example

Updating load balancer backend instances without outage.

### Interview Punch Lines

-   "Creates safe transition window."
-   "Avoids service disruption."

------------------------------------------------------------------------

## 60. What is **ignore_changes**?

Tells Terraform to ignore certain attributes during comparison with
state.

### Example

``` hcl
lifecycle {
  ignore_changes = [tags]
}
```

### Real-World Example

Autoscaling adjusts instance size without Terraform reverting changes.

### Interview Punch Lines

-   "Prevents unnecessary updates."
-   "Supports external modifications."
