## **36. What is module?**

A **module** in Terraform is a container that groups multiple
**resources together into a reusable unit**. Instead of writing the same
**infrastructure code repeatedly**, we package related resources into a
module and reuse it across different deployments.

Every Terraform configuration is technically a module. The main
configuration we execute is called the **root module**, and additional
modules we call inside it are **child modules**.

Modules improve **organization, readability, and maintainability**. They
allow teams to **standardize infrastructure patterns** and reduce
duplication.

They also support **abstraction**, meaning users of the module don't
need to understand internal resource details --- they only provide
**input variables**.

**Real-World Example**

A module that creates a complete **web server stack including network,
compute, and security settings** reused across multiple projects.

**Interview Line**

"A Terraform module groups resources into reusable infrastructure
components."

------------------------------------------------------------------------

## **37. Why modules used?**

Modules are used to improve **code reuse** and maintain **consistency
across infrastructure deployments**.

Benefits include:

**avoiding duplicate code**

**enforcing standards**

**simplifying maintenance**

**improving collaboration**

**enabling abstraction**

Without modules, managing large infrastructure becomes difficult because
**similar configurations are repeated and hard to update**.

Modules allow **centralized updates** that propagate across
environments.

**Real-World Example**

Updating **security group rules** in one module automatically affects
all deployments using it.

**Interview Line**

"Modules promote reuse, consistency, and maintainability."

------------------------------------------------------------------------

## **38. Root module vs child module**

The **root module** is the main Terraform configuration directory where
commands are executed. It orchestrates **infrastructure creation** and
calls other modules.

**Child modules** are reusable modules referenced by the root module.
They contain grouped resources that perform specific tasks.

Root module acts as **controller**, child modules act as **building
blocks**.

Understanding this separation helps structure **complex deployments
effectively**.

**Real-World Example**

Root module deploys **application infrastructure** while child modules
handle **networking or database provisioning**.

**Interview Line**

"Root module coordinates execution; child modules implement reusable
components."

------------------------------------------------------------------------

## **39. Module versioning**

**Module versioning** ensures consistent module behavior across
deployments. When modules are sourced remotely, **version numbers**
define which module release Terraform should use.

Versioning prevents **unexpected changes** caused by updates and
supports **rollback** if issues occur.

It provides **stability and traceability** in infrastructure pipelines.

Managing versions carefully is important for **production reliability**.

**Real-World Example**

Locking module version in production while testing newer version in
staging.

**Interview Line**

"Module versioning guarantees stable and predictable deployments."

------------------------------------------------------------------------

## **40. How to pass variables to module?**

Variables are passed to modules through **input parameters** when the
module is called.

This allows **customization of module behavior** without modifying
module code.

Passing variables enables **flexible deployments** while preserving
module reusability.

**Outputs from modules** can also be captured and used by other modules
or root configuration.

**Real-World Example**

Passing **instance size and region values** to infrastructure module.

**Interview Line**

"Variables customize module execution without altering module
internals."

------------------------------------------------------------------------

## **41. Reusable infra example**

Reusable infrastructure modules are used when multiple environments
share similar **architecture patterns**.

Instead of rewriting code for each environment, one module defines the
infrastructure and is reused with **different inputs**.

This reduces **duplication** and ensures **consistency**.

Reusable modules are foundational for **scalable DevOps practices**.

**Real-World Example**

Single **VPC module reused for dev, staging, and production** with
different CIDR blocks.

**Interview Line**

"Reusable modules standardize infrastructure across environments."

------------------------------------------------------------------------

## **42. Public Terraform Registry**

The **public Terraform Registry** hosts community and vendor-maintained
modules that can be used directly.

It allows engineers to reuse **tested infrastructure modules** instead
of building from scratch.

Registry modules accelerate **development** and encourage **best
practices**.

However, modules should be reviewed for **quality and security** before
production use.

**Real-World Example**

Using registry module to deploy **Kubernetes cluster** quickly.

**Interview Line**

"Registry modules accelerate infrastructure deployment."

------------------------------------------------------------------------

## **43. Private modules**

**Private modules** are internally developed modules shared within an
organization.

They encapsulate **company standards, compliance requirements, and
architectural patterns**.

Using private modules ensures **consistency and governance across
teams**.

They are typically stored in **internal repositories**.

**Real-World Example**

Company-specific **networking module** used across all projects.

**Interview Line**

"Private modules enforce organizational infrastructure standards."

------------------------------------------------------------------------

## **44. How to structure Terraform project?**

Proper **project structure** improves **maintainability and
collaboration**.

Common structure includes:

**separating modules**

**organizing environment directories**

**isolating configuration layers**

**managing state properly**

Good structure simplifies **scaling infrastructure complexity**.

Clear organization helps **onboarding and debugging**.

**Real-World Example**

Separate directories for **networking, compute, and environment
configs**.

**Interview Line**

"Well-structured projects improve scalability and teamwork."

------------------------------------------------------------------------

## **45. Multi-environment using modules?**

Modules enable **multi-environment deployments** by allowing the same
infrastructure logic to be reused with different inputs.

Each environment passes **unique variables** while using identical
module code.

This ensures **consistency** while maintaining **environment
isolation**.

It simplifies scaling deployments across **multiple stages**.

**Real-World Example**

Dev, staging, and production using same module but different
configuration values.

**Interview Line**

"Modules enable consistent multi-environment deployments."
