## **1. What is Terraform and why is it used?**

**Terraform** is an open-source Infrastructure as Code (IaC) tool
developed by **HashiCorp** that allows you to **define, provision, and
manage infrastructure** using **configuration files** instead of manual
processes.

Rather than logging into cloud consoles and clicking through steps to
create **servers, networks, or storage**, Terraform allows engineers to
write **infrastructure definitions in code**. Terraform then
communicates with **cloud provider APIs** to create or update those
resources automatically.

It is widely used because it provides:

**Automation of infrastructure provisioning**\
**Repeatable and consistent environments**\
**Version control for infrastructure changes**\
**Multi-cloud capability**\
**Infrastructure lifecycle management**

Terraform also uses a **declarative approach**, meaning we describe the
**desired infrastructure state** and Terraform figures out how to reach
it.

**Real-World Example**

A DevOps team provisions complete AWS environments including **VPC, EC2,
load balancers, and databases** automatically using Terraform scripts in
**CI/CD**.

**Interview Punch Lines**

"Terraform automates infrastructure provisioning using code."\
"It enables reproducible, version-controlled infrastructure."
------------------------------------------------------------------------

## **2. What is IaC?**

**Infrastructure as Code (IaC)** is the practice of managing
infrastructure through **code instead of manual configuration**.

Traditionally, infrastructure setup involved manual work, leading to
**inconsistencies and errors**. IaC solves this by allowing
infrastructure definitions to be **stored, versioned, and reused** just
like application code.

Benefits include:

**Consistency across environments**\
**Faster deployment**\
**Easier rollback**\
**Improved collaboration**\
**Reduced human error**

IaC tools interpret configuration files and apply changes automatically.

**Real-World Example**

Creating identical **staging and production environments** using the
same Terraform code.

**Interview Punch Lines**

"IaC treats infrastructure like software."\
"It ensures automation and consistency."
------------------------------------------------------------------------

## **3. Terraform vs Ansible?**

Terraform and Ansible serve different roles in **DevOps workflows**.

Terraform focuses on **infrastructure provisioning**. It creates
resources like **networks, servers, and storage** using a **declarative
approach**.

Ansible focuses on **configuration management**. It configures systems
after infrastructure exists, using **procedural task execution**.

Terraform answers:\
**"What infrastructure should exist?"**

Ansible answers:\
**"How should that infrastructure be configured?"**

Often they are used together in pipelines.

**Real-World Example**

Terraform creates **EC2 instances**, Ansible installs **application
dependencies**.

**Interview Punch Lines**

"Terraform builds infrastructure."\
"Ansible configures infrastructure."
------------------------------------------------------------------------

## **4. What is provider?**

A **provider** is a **plugin** that enables Terraform to interact with
external platforms like **AWS, Azure, or Kubernetes**.

Providers translate Terraform configuration into **API calls**. Each
provider understands how to manage **resources within its platform**.

Without providers, Terraform would have no way to create or manage
infrastructure.

Providers also define available **resource types and configuration
options**.

**Real-World Example**

AWS provider enabling creation of **EC2 instances**.

**Interview Punch Lines**

"Providers connect Terraform to infrastructure APIs."\
"They enable multi-cloud management."
------------------------------------------------------------------------

## **5. What is resource block?**

A **resource block** defines infrastructure components Terraform should
manage.

It specifies:

**resource type**\
**configuration parameters**\
**desired state**

Terraform reads resource blocks to **create, modify, or delete
infrastructure**.

Resource blocks are the **fundamental building units** of Terraform
configuration.

**Real-World Example**

Defining a resource block to create a **virtual server**.

**Interview Punch Lines**

"Resource blocks describe infrastructure units."\
"They define what Terraform should create."
------------------------------------------------------------------------

## **6. What is state file?**

Terraform maintains a **state file** that records the **current
infrastructure managed by Terraform**.

The state tracks:

**created resources**\
**metadata**\
**dependencies**\
**mappings between config and real infrastructure**

Terraform uses state to understand what exists so it can **calculate
changes accurately**.

Without state, Terraform would not know how to update infrastructure
safely.

**Real-World Example**

State file ensuring Terraform **updates existing servers rather than
recreating them**.

**Interview Punch Lines**

"State maps configuration to real infrastructure."\
"It enables incremental updates."
------------------------------------------------------------------------

## **7. Why state file important?**

The **state file** is critical because Terraform relies on it for
**decision-making**.

It allows Terraform to:

**detect changes**\
**maintain resource relationships**\
**plan accurate updates**\
**avoid duplication**

State also supports **dependency resolution and performance
optimization**.

Protecting state is important because losing it may cause
**infrastructure inconsistency**.

**Real-World Example**

Corrupted state leading to **incorrect infrastructure changes**.

**Interview Punch Lines**

"State is Terraform's source of truth."\
"It ensures safe infrastructure changes."
------------------------------------------------------------------------

## **8. What is terraform init?**

**terraform init** initializes a **working directory**.

It prepares Terraform by:

**downloading providers**\
**configuring backend**\
**installing modules**

This must be executed before **planning or applying configurations**.

Initialization ensures Terraform has everything required to **interact
with infrastructure**.

**Real-World Example**

Running init after **cloning Terraform repository**.

**Interview Punch Lines**

"Init prepares execution environment."\
"It installs dependencies."
------------------------------------------------------------------------

## **9. terraform plan vs apply?**

**Plan**

**previews infrastructure changes**\
**validates configuration**\
**shows add/modify/delete actions**

**Apply**

**executes the changes**\
**provisions infrastructure**\
**updates state**

Separating planning and execution provides **safety**.

**Real-World Example**

Reviewing changes before applying to **production**.

**Interview Punch Lines**

"Plan previews changes."\
"Apply performs changes."
------------------------------------------------------------------------


## **10. terraform destroy?**

**terraform destroy** removes all managed resources defined in
configuration.

It calculates resources tracked in **state** and deletes them.

Used for:

**cleanup**\
**cost control**\
**temporary environments**

This ensures **lifecycle automation**.

**Real-World Example**

Deleting **testing environment** after completion.

**Interview Punch Lines**

"Destroy automates teardown."\
"It manages full lifecycle."
------------------------------------------------------------------------

## **11. Where is state stored by default?**

By default, Terraform stores state **locally in the working directory**.

This simple setup works for individuals but introduces risks:

**no collaboration**\
**no locking**\
**risk of loss**

Production setups typically move state to **remote storage**.

**Real-World Example**

Local state used during development.

**Interview Punch Lines**

"Default state storage is local."\
"Not suitable for team environments."
------------------------------------------------------------------------

## **12. What is backend?**

A **backend** defines how Terraform **stores state and executes
operations**.

It determines:

**state location**\
**locking behavior**\
**collaboration support**

Backends allow switching between **local and remote state management**.

**Real-World Example**

Centralized state enabling **team deployment workflows**.

**Interview Punch Lines**

"Backend manages state storage."\
"It enables collaboration."
------------------------------------------------------------------------

## **13. Local vs remote backend**

**Local Backend**

**state on local machine**\
**simple**\
**single-user use**

**Remote Backend**

**centralized storage**\
**state locking**\
**collaboration enabled**\
**more secure**

Remote backends improve **reliability and teamwork**.

**Real-World Example**

Team deployments sharing **centralized state**.

**Interview Punch Lines**

"Local for testing."\
"Remote for production."
------------------------------------------------------------------------

## **14. What is .terraform folder?**

The **.terraform directory** is created during initialization.

It stores:

**downloaded providers**\
**module code**\
**backend metadata**

It acts as a **cache and execution workspace**.

Deleting it does not affect infrastructure; it can be recreated.

Usually excluded from **version control**.

**Real-World Example**

Provider plugins stored locally to **avoid repeated downloads**.

**Interview Punch Lines**

".terraform stores dependencies."\
"It supports execution environment."
------------------------------------------------------------------------

## **15. What is lock file (.terraform.lock.hcl)?**

The **lock file** records exact **provider versions used**.

It ensures:

**consistent environments**\
**reproducible deployments**\
**dependency stability**

Without it, environments might use different provider versions.

It should be committed to **version control**.

**Real-World Example**

CI/CD pipelines producing **consistent infrastructure**.

**Interview Punch Lines**

"Lock file ensures version consistency."\
"Prevents unexpected upgrades."
